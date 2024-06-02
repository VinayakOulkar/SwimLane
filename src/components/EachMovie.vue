<template>
    <div id="EachMovie" class="">
        <!-- Movie Image -->
        <img :src="ImagePath" :alt="ImageName" loading="eager"/>
        <div class="Content m-3">
          <!-- New -->
          <div class="new pb-1"><span :class="{ 'hidden': type !== 'NEW' }">NEW</span></div>
          <!-- Movie Name -->
          <div class="MovieName">
            <div class="ImageName pt-1">{{ImageName1}}</div>
            <div class="ImageName">{{ImageName2}}</div>
          </div>
        </div>
    </div>
</template>

<script>

export default {
  name: 'EachMovie',
  props:{
    ImagePath:String,
    type:String,
    ImageName1:String,
    ImageName2:String
  }
}
</script>

<style scoped>

.new{
  background: linear-gradient(to right,rgba(28, 28, 30, 1),rgba(18, 18, 18, 1));
}

#EachMovie
{
  width: 13.438rem;
  height: 58vh;
  border-radius: 10px;
  overflow: hidden;
  color: white;
  background: linear-gradient(to right,rgba(28, 28, 30, 1),rgba(18, 18, 18, 1));
}

#EachMovie img
{
  width: 13.438rem;
  height: 40vh;
  overflow: hidden;
}

.new span
{
  font-size: 0.8rem;
  font-weight: 800;
  color:rgba(28, 28, 30, 1);
  background-color: rgba(255, 159, 10, 1);
  border-radius: 3px;
  letter-spacing: 0.1rem;
  text-align: center;
  padding-top: 0.15rem;
  padding-bottom: 0.15rem;
  padding-left: 0.5rem;
  padding-right: 0.5rem;
}

.ImageName
{
  font-size: 1rem;
  background: linear-gradient(to right,rgba(28, 28, 30, 1),rgba(18, 18, 18, 1));
  font-weight: 500;
}

.MovieName
{
  line-height: 2rem;
}

.hidden {
  visibility:hidden;
}

/* For Tablet & Desktop */
@media screen and (min-width: 768px) {
  #EachMovie
  {
    width: 21.438rem;
    height: 41.25rem;
    border-radius: 10px;
    overflow: hidden;
    color: white;
    background: linear-gradient(to right,rgba(28, 28, 30, 1),rgba(18, 18, 18, 1));
  }

  #EachMovie img
  {
    width: 21.438rem;
    height: 32.125rem;
    overflow: hidden;
  }

  .new span
  {
    font-size: 1.27rem;
    font-weight: 800;
    color:rgba(28, 28, 30, 1);
    background-color: rgba(255, 159, 10, 1);
    border-radius: 3px;
    letter-spacing: 0.1rem;
    text-align: center;
    padding-top: 0.15rem;
    padding-bottom: 0.15rem;
    padding-left: 0.5rem;
    padding-right: 0.5rem;
  }

  .ImageName
  {
    font-size: 1.5rem;
    background: linear-gradient(to right,rgba(28, 28, 30, 1),rgba(18, 18, 18, 1));
    font-weight: 500;
  }
}

</style>
