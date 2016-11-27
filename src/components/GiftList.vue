<template>

    <section class="container" >
        <div class="row">
            <template v-for="gift in gifts">
              <div class="gift col-md-4 col-xs-6 animated fadeIn">
                <div class="gift__thumb">
                  <div class="gift__thumb--hover"></div>
                  <div class="gift__thumb--hover-text text-center">
                      <div>Customize &amp; <br>make it yours!</div>
                  </div>
                  <img v-bind:src="gift.image">
                </div>
                <div class="gift__title text-center" >{{gift.title}}</div>
                <div class="gift__price text-center" >${{gift.price}}</div>
              </div>
            </template>
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
  data() {
    return {
      gifts: generateFakeGifts(),
      filters: [],
    };
  },
};
</script>


<style scoped>
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
  .gift__title, .gift__price{
    font-weight: bold;
    color: gray;
    font-size: 20px;
  }
</style>
