<template>
  <div>
    <!-- <b-form-group label="Select calendar interactive state" v-slot="{ ariaDescribedby }">
      <b-form-radio-group
        v-model="state"
        :aria-describedby="ariaDescribedby"
        aria-controls="ex-disabled-readonly"
      >
        <b-form-radio value="disabled">Disabled</b-form-radio>
        <b-form-radio value="readonly">Readonly</b-form-radio>
        <b-form-radio value="normal">Normal</b-form-radio>
      </b-form-radio-group>
    </b-form-group> -->

    <b-calendar></b-calendar>
    <b-button v-b-toggle.collapse-1 variant="primary">Toggle Collapse</b-button>
    <b-collapse id="collapse-1" class="mt-2">
        <b-card>
        <p class="card-text">Collapse contents Here</p>
        <b-button v-b-toggle.collapse-1-inner size="sm">Toggle Inner Collapse</b-button>
        <b-collapse id="collapse-1-inner" class="mt-2">
            <b-card>Hello!</b-card>
        </b-collapse>
        </b-card>
    </b-collapse>
    <div v-for="item in testData" :key="item.id">
        <div>{{ item.begin }}</div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
  export default {
    data() {
      return {
        state: 'disabled',
        testData: []
      }
    },
    computed: {
      disabled() {
        return this.state === 'disabled'
      },
      readonly() {
        return this.state === 'readonly'
      }
    },
    mounted () {
        axios.get('https://www.travel.taipei/open-api/zh-tw/Events/Activity?begin=2021-03-24&end=2021-05-05&page=1')
        .then((res) => {
            console.log(res)
            // console.log(res.data.data[0].description)
            let wholedata = res.data.data
            wholedata.forEach((el, id, ar) =>{
                // console.log(el.description)
                console.log(el)
                console.log(id)
                console.log(ar)
                this.testData.push(el)
            })
        })
        .catch((err) => console.log(err) )
    }
  }
</script>

