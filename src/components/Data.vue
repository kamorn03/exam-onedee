<template>
  <div>
    <!-- JSON -->
    <b-container id="json">
      <pre class="code code-jquery"><label>JSON</label>
      <code>{{ json }}</code>
       </pre>
    </b-container>
  </div>
</template>

<script>
import json from "../json/data.json";
export default {
  components: {},
  data() {
    return {
      json: json,
    };
  },
  mounted() {
    // let obj = {};
    if (this.json) {
      //   this.json = this.json.map((format) => {
      //     obj.name = format.data.name;
      //     return this.dedup_and_sum(format.data, "name");
      //   });

      this.json = this.json[0];
      let dedup = this.dedup_and_sum(this.json.data, "name");
      console.log(dedup);

      this.json = dedup.map((item) => ({
        id: item.id,
        name: item.name,
        price: item.price,
        amount: item.order.amount,
      }));
    }
  },
  methods: {
    dedup_and_sum(arr, prop) {
      var seen = {},
        order = [];
      arr.forEach(function (o) {
        var id = o[prop];
        if (id in seen) {
          // keep running sum of stocklevel
          var stocklevel = seen[id].stocklevel + o.stocklevel;
          // keep this newest record's values
          seen[id] = o;
          // upid[118805291], stocklevel=432, instock=truedate stocklevel to our running total
          seen[id].stocklevel = stocklevel;
          // keep track of ordering, having seen again, push to end
          order.push(order.splice(order.indexOf(id), 1));
        } else {
          seen[id] = o;
          order.push(id);
        }
      });

      return order.map(function (k) {
        return seen[k];
      });
    },
    // idsAreEqual(obj1, obj2) {
    //   return obj1.id === obj2.id;
    // },
    // arrayContains(arr, val, equals) {
    //   var i = arr.length;
    //   while (i--) {
    //     if (equals(arr[i], val)) {
    //       return true;
    //     }
    //   }
    //   return false;
    // },
    // removeDups(arr, equals) {
    //   var originalArr = arr.slice(0);
    //   //   var i, k, len, val;
    //   var i, val;
    //   arr.length = 0;
    //   for (i = originalArr.length - 1;   i > 0;--i) {
    //     val = originalArr[i];
    //     if (!this.arrayContains(arr, val, equals)) {
    //       arr.push(val);
    //     }
    //   }
    // },
  },
  name: "Data",
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

#wrapper {
  padding: 5%;
  margin: 0 auto;
}

/* CSS Simple Pre Code */
pre {
  background: #333;
  white-space: pre;
  word-wrap: break-word;
  overflow: auto;
}

pre.code {
  margin: 20px 25px;
  border-radius: 4px;
  border: 1px solid #292929;
  position: relative;
}

pre.code label {
  font-family: sans-serif;
  font-weight: bold;
  font-size: 13px;
  color: #ddd;
  position: absolute;
  left: 1px;
  top: 15px;
  text-align: center;
  width: 60px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  pointer-events: none;
}

pre.code code {
  font-family: "Inconsolata", "Monaco", "Consolas", "Andale Mono",
    "Bitstream Vera Sans Mono", "Courier New", Courier, monospace;
  display: block;
  margin: 0 0 0 60px;
  padding: 15px 16px 14px;
  border-left: 1px solid #555;
  overflow-x: auto;
  font-size: 13px;
  line-height: 19px;
  color: #ddd;
}

pre::after {
  content: "double click to selection";
  padding: 0;
  width: auto;
  height: auto;
  position: absolute;
  right: 18px;
  top: 14px;
  font-size: 12px;
  color: #ddd;
  line-height: 20px;
  overflow: hidden;
  -webkit-backface-visibility: hidden;
  transition: all 0.3s ease;
}

pre:hover::after {
  opacity: 0;
  visibility: visible;
}

pre.code-jquery code {
  text-align: left;
  color: #4dd0e1;
}
</style>
