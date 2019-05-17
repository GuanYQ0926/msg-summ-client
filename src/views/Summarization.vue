<template>
  <!-- <div> -->
    <canvas id="summarization"></canvas>
  <!-- </div> -->
</template>

<script>
import axios from 'axios'
import WordCloud from 'wordcloud'

export default {
  name: 'Summarization',
  data() {
    return{}
  },
  methods: {
    getMessage() {
      const path = 'http://localhost:5000/summarization'
      axios.get(path)
        .then(res => {
          const data = res.data
          console.log(`response: ${data}`);
          // render wordcloud
          const canvas = document.getElementById('summarization')
          const length = Math.min(window.innerWidth, window.innerWidth*0.6)
          canvas.width = length
          canvas.height = length
          const dataList = []
          for(const word in data) {
            dataList.push([word, data[word]])
          }
          WordCloud.minFontSize = '25px'
          WordCloud(canvas, {list: dataList})
        })
        .catch(err => {
          console.log(err)
        })
    },
  },
  created() {
    this.getMessage()
  },
}
</script>
