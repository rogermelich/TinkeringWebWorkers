<template>
    <p>Count numbers: </p>
    <button onclick="startWorker()">Start Worker</button>
    <button onclick="stopWorker()">Stop Worker</button>
</template>

<script>
    var w
    export default {
      name: 'counter',
      data () {
        return {
          counter: 0
        }
      },
      methods: {
        startWorker () {
          if (typeof (Worker) !== 'undefined') {
            if (typeof (w) === 'undefined') {
              w = new Worker('js/counter.js')
            }
            w.onmessage = function (event) {
              document.getElementById('result').innerHTML = event.data
            }
          } else {
            document.getElementById('result').innerHTML = 'Sorry! No Web Worker support.'
          }
        },
        stopWorker () {
          w.terminate()
          w = undefined
        }
      }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h1, h2 {
        font-weight: normal;
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
</style>
