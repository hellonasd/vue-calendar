<template>
  <div class="date">
    <div class="date__wrapper">
      <div class="date__calendar">
        <h3 class="date__year">{{ value.format("MMMM") }}</h3>
        <span class="date__number">{{ value.format("YYYY") }}</span>
      </div>
      <div class="date__navigation">
        <button class="date__arrow-left" @click="prev">&lt;</button>
        <button class="date__today" @click='today'>Today</button>
        <button class="date__arrow-right" @click="next">&gt;</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["value"],
  methods : {
    next(){
      this.$emit('next');
      this.$forceUpdate();
    },
    prev(){
      this.$emit('prev'),
      this.$forceUpdate();
    },
    today(){
      this.$emit('today');
      this.$forceUpdate();
    }
  }
};
</script>

<style lang='scss' scoped>
.date {
  &__wrapper {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  &__calendar {
    display: flex;
    align-items: center;
  }
  &__year {
    font-size: 40px;
    margin-right: 10px;
    text-transform: capitalize;
    color: gray;
  }
  &__number {
    font-size: 50px;
    color: gray;
  }
  &__arrow-left {
    background-color: #595a5c;
    width: 30px;
    height: 20px;
    border: none;
    border-radius: 5px;
    margin-right: 2px;
    color: white;
    cursor: pointer;
  }
  

  &__today {
    background-color: #595a5c;
    width: 50px;
    height: 20px;
    border: none;
    border-radius: 5px;
    margin: 0px 2px 0px 0px;
    color: white;
    cursor: pointer;
  }
  &__arrow-right {
    background-color: #595a5c;
    width: 30px;
    height: 20px;
    border: none;
    border-radius: 5px;
    margin-right: 10px;
    color: white;
    cursor: pointer;
  }
}
</style>