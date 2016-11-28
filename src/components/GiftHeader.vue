<template>
  <header class="fadeInDown animated">
    <div class="container header">
      <img class="header__gliter-left fadeInDown animated " src="../assets/Glitter_Top-Left.png">
      <img class="header__gliter-right fadeInDown animated " src="../assets/Glitter_Top-Right.png">
      <div class="header__title"><span class="line">Find the</span> <span class="line">perfect gift</soan> <span class="line">for your</span></div>
      <div class="header__middle fadeIn animated" >

        <img class="header__red-cup" src="../assets/TopCharm-RedCup.png">
        <img class="header__words" src="../assets/words.gif">
        <img class="header__north-star" src="../assets/TopCharm-NorthStar.png">
        <img class="header__heart rotateIn animated delay2seconds hidden-sm hidden-xs" src="../assets/TopCharm-GoldHeart.png">
      </div>
      <div class="fadeIn animated delay1second">
        <div class="header__filter-text">Start personalizing your gift with:</div>
        <div class="header__filters">

          <div class="row">
                <div class="col-xs-12 col-sm-12 col-md-9">
                    <div class="row">
                      <div class="col-xs-6 col-sm-4 col-md-6">
                          <button @click="toggleFilter('family')"  v-bind:class="{ 'selected': isFilterActive('family') !== -1 }" class="header__btn">Family</button>
                      </div>
                      <div class="col-xs-6 col-sm-4 col-md-6">
                          <button @click="toggleFilter('love')"  v-bind:class="{ 'selected': isFilterActive('love') !== -1 }"  class="header__btn">Love</button>
                      </div>
                      <div class="col-xs-6 col-sm-4 col-md-6">
                        <button @click="toggleFilter('faith')"  v-bind:class="{ 'selected': isFilterActive('faith') !== -1 }"  class="header__btn">Faith</button>
                      </div>
                      <div class="col-xs-6 col-sm-4 col-md-6">
                        <button @click="toggleFilter('hobbies')"  v-bind:class="{ 'selected': isFilterActive('hobbies') !== -1 }"  class="header__btn">Hobbies</button>
                      </div>
                      <div class="col-xs-6 col-sm-4 col-md-6">
                        <button @click="toggleFilter('purpose')"  v-bind:class="{ 'selected': isFilterActive('purpose') !== -1 }"  class="header__btn">Purpose</button>
                      </div>
                      <div class="col-xs-6 col-sm-4 col-md-6">
                        <button @click="toggleFilter('engraving')"  v-bind:class="{ 'selected': isFilterActive('engraving') !== -1 }"  class="header__btn">Engraving</button>
                      </div>
                  </div>
                </div>
                <div class="col-xs-12 col-sm-12 col-md-3">
                        <button @click="toggleFilter('grabngo', true)"  v-bind:class="{ 'selected': isFilterActive('grabngo') !== -1 }"  class="header__btn header__btn--grab">Grab-N-Go Gifts</button>
                </div>
            </div>



        </div>
      </div>


    </div>
  </header>
</template>

<script>
export default {
  data() {
    return {
      activeFilters: [],
    };
  },
  methods: {
    isFilterActive(filterName) {
      return this.activeFilters.indexOf(filterName);
    },
    toggleFilter(filterName, clearAll) {
      const isActive = this.isFilterActive(filterName);
      if (isActive !== -1) {
        this.activeFilters.splice(isActive, 1);
      } else {
        if (clearAll) {
          this.activeFilters = [];
        } else if (this.activeFilters[0] === 'grabngo') { // FIXME
          this.activeFilters = [];
        }
        this.activeFilters.push(filterName);
      }
      this.$emit('filtersChanged', this.activeFilters.slice());
    },
  },
};
</script>


<style >
header{
  position: relative;
  background: rgba(22,21,49,1);
  background: linear-gradient(to right, rgba(22,21,49,1) 0%, rgba(68,74,122,1) 38%, rgba(68,74,122,1) 50%, rgba(68,74,122,1) 66%, rgba(22,21,49,1) 100%);
  filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#161531', endColorstr='#161531', GradientType=1 );
}
.container {
  position: relative;
}

.header__gliter-left{
  position: absolute;
  top: -30px;
  left: 0;
}

.header__gliter-right{
  position: absolute;
  top: -30px;
  right: 0;
}
.header__title{
  margin-top: 40px;
  color: #c2c6ce;
  text-align: center;
  font-size: 35px;
}
.header__heart{
  position: absolute;
  bottom: -50px;
  left: -50px;
}

.header__north-star{
  position: absolute;
  bottom: 0;
  right: 0;
}
.header__red-cup{
  position: absolute;
  bottom: 0;
  left: 0;
}

span.line {
  display: inline-block;
}
.header__filter-text{
  font-size: 20px;
  margin-bottom: 20px;
  font-family: 'Rokkitt', serif;
  text-align: center;
  color: #c2c6ce;
}
.header__middle{
  max-width: 400px;
  position: relative;
  text-align: center;
  margin-left: auto;
  margin-right: auto;
}
.header__filters{
  margin-bottom: 20px;
  text-align: center;
}
.header__btn{
  transition: background-color 0.5s ease;
  border: 0px;
  padding: 10px;
  outline: none;
  margin: 5px;
  width: 100%;
  color: #012453;
  background-color: white;
}
.header__btn.selected{
  color: white;
  background-color: #7499c6;
}
.header__btn:hover{
  color: white;
  background-color: #7fa6d4;
}


@media (min-width: 780px) { 
  .header__btn--grab{
    width: 400px;
  }
 }


@media (min-width: 992px) { 
  .header__btn--grab{
    height: 140px;
  }
}



</style>
