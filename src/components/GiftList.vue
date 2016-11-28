<template>

    <section class="container" >
       <div class="row">
         <div class="col-sm-6 col-sm-offset-6 col-xs-12 col-md-4 col-md-offset-8 sort-combo">
          <select v-model="sortKey" @change="sort">
            <option value="title"> Sort by: Title</option>
            <option value="price"> Sorty by: Price</option>
          </select>
         </div>
       </div>
        <div class="row">
            <transition-group name="list" tag="div" appear>
              <div v-for="(gift, index) in filteredResults(gifts)" class="list-item gift col-md-4 col-xs-6" v-bind:key="gift.id">
                  <div class="gift__thumb">
                    <div class="gift__thumb--hover"></div>
                    <div class="gift__thumb--hover-text">
                        <div>Customize &amp; <br>make it yours!</div>
                    </div>
                    <img v-bind:src="gift.image" >
                  </div>
                  <div class="gift__text">
                    <div class="gift__text__title" >{{gift.title}}</div>
                    <div class="gift__text__price" >${{gift.price}}</div>
                  </div>
              </div>
            </transition-group>
             <div class="gift col-md-4 col-xs-6">
                 <div class="gift__thumb"><img class="gift__thumb" src="../assets/thumbs/t6.jpg"></div>
            </div>
        </div>


    </section>

</template>

<script>
import t1 from '../assets/thumbs/t1.jpg';
import t2 from '../assets/thumbs/t2.jpg';
import t3 from '../assets/thumbs/t3.jpg';
import t4 from '../assets/thumbs/t4.jpg';
import t5 from '../assets/thumbs/t5.jpg';

function generateFakeGifts() {
  function getRandomItem(arr) {
    return arr[Math.floor(Math.random() * arr.length)];
  }
  function getRandomItems(arr, howMany) {
    const items = [];
    const myArr = arr.slice();
    for (let i = 0; i < howMany; i += 1) {
      const index = Math.floor(Math.random() * myArr.length);
      items.push(myArr.splice(index, 1)[0]);
    }
    return items;
  }
  const images = [t1, t2, t3, t4, t5];
  const tags = ['family', 'love', 'faith', 'hobbies', 'purpose', 'engraving', 'grabngo'];
  const gifts = [];
  for (let i = 0; i < 20; i += 1) {
    const tag = getRandomItems(tags, 3);
    const gift = {
      id: i,
      image: getRandomItem(images),
      tags: tag,
      title: tag.join(' '),
      price: Math.floor(((Math.random() * (90 - 10)) + 10)),
    };
    gifts.push(gift);
  }
  return gifts;
}

export default {
  mounted() {
    this.sort();
  },
  methods: {
    sort() {
      this.gifts.sort((a, b) => {
        if (a[this.sortKey] < b[this.sortKey]) return -1;
        if (a[this.sortKey] > b[this.sortKey]) return 1;
        return 0;
      });
    },
    filteredResults() {
      let filteredResults = this.gifts;
      if (this.filters.length > 0) {
        filteredResults =
          this.gifts.filter(gift => gift.tags.some(tag => this.filters.includes(tag)));
      }
      return filteredResults;
    },
  },
  data() {
    return {
      sortKey: 'title',
      gifts: generateFakeGifts(),
      filters: [],
    };
  },
};
</script>


<style scoped>
  .row {
    position: relative;
  }
  .container{
    margin-bottom: 30px;
  }
  .gift{
    margin-top: 30px;
    overflow: hidden;
  }
  .gift__thumb:hover .gift__thumb--hover {     opacity: 0.7; }
  .gift__thumb:hover .gift__thumb--hover-text {     opacity: 1; }

  .gift__thumb{
    position: relative;
    cursor: pointer;
  }
  .gift__thumb--hover{
    transition: opacity 0.5s ease-in-out;
    border: 20px solid gray;
    background-color: white;
    opacity: 0;
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    width: 100%;
    z-index: 20;
  }
  .gift__thumb--hover-text{
    text-align: center;
    transition: opacity 0.5s ease-in-out;
    opacity: 0;
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    width: 100%;
    z-index: 50;
  }
  .gift__thumb--hover-text div{
    line-height: 20px;
    font-size: 20px;
    font-family: 'Rokkitt', serif;
    position: absolute;
    top: 58%;
    left: 50%;
    height: 30%;
    width: 50%;
    margin: -15% 0 0 -25%;
  }
  .gift__thumb img{
    width: 100%;
  }
  .gift__text{
    text-align: center;
    font-weight: bold;
    color: gray;
    font-size: 20px;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  .list-item {
    display: inline-block;
    transition: all 0.5s;
  }
  .list-enter, .list-leave-active {
    opacity: 0;
  }
  .list-leave-active {
    display: none;
  }
  .sort-combo{
    margin-top: 30px;
  }
  .sort-combo select{
    width: 100%;
    font-size: 20px;
    background-color: white;
    border: 1px solid lightgrey;
    padding: 10px;
    border-radius: 0;
    -webkit-appearance: none;
    outline: none;
  }
  @media only screen and (max-width: 500px) {
    .gift__text{
      height: 40px;
      font-size: 15px;
    }
  }


</style>

