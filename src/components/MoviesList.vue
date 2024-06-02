<template>
    <div id="main" class="py-5">
      <!-- Heading -->
      <p id="main_heading" class="pt-4 pb-3">Most-watched films</p>
        
      <div>
        <div class="carousel-inner d-flex">
          <!-- All Movies -->
          <div id="EachMovieContainer" class="d-flex"> 
            <EachMovie class="ScrollContainer" v-for="(image, index) in images" :key="index"
               :ImagePath="image.Movie_Path" :type="image.type"
               :ImageName1="image.Movie_Name1" :ImageName2="image.Movie_Name2" />
          </div>
          
        </div>
        <!-- Previous Button -->
        <button @click="moveDivRight" class="carousel-control-prev" type="button" >
          <span class="carousel-control-prev-icon" aria-hidden="true"></span>
          <span class="visually-hidden">Previous</span>
        </button>
        <!-- Next Button -->
        <button @click="moveDivLeft" class="carousel-control-next" type="button" data-bs-target="#carouselExampleControls" data-bs-slide="next">
          <span class="carousel-control-next-icon" aria-hidden="true"></span>
          <span class="visually-hidden">Next</span>
        </button>
      </div>
    </div>
</template>

<script>
import EachMovie from './EachMovie.vue';

export default {
  name: 'MoviesList',
  components: {
    EachMovie
  },
  mounted(){
    window.addEventListener('keydown', this.handleKeyPress);
    let divs = document.querySelectorAll('#EachMovie');
    for (var i = 0; i < divs.length; i++) 
    {
      // Set the index value as a div attribute
      divs[i].setAttribute('div-index', i);
    }
  },
  data()
  {
    return {
      left:false,
      right:false,
      currentIndex: -1,
      scrollValue:0,
      remValue:0,
      rootFontSize:0,
      click_sound:new Audio(require('@/assets/Music/click_sound.wav')),
      images:{
        Img1:{
          Movie_Path: require('@/assets/Images/Oppenheimer.jpg'),
          type:" ",
          Movie_Name1: "Oppenheimer",
          Movie_Name2: " "
        },
        Img2:{
          Movie_Path: require('@/assets/Images/PastLives.jpg'),
          type:" ",
          Movie_Name1: "Past Lives",
          Movie_Name2: " "
        },
        Img3:{
          Movie_Path: require('@/assets/Images/PoliteSociety.png'),
          type:" ",
          Movie_Name1: "Polite Society",
          Movie_Name2: " "
        }
        ,
        Img4:{
          Movie_Path: require('@/assets/Images/Robots.png'),
          type:" ",
          Movie_Name1: "Robots",
          Movie_Name2: " "
        },
        Img5:{
          Movie_Path: require('@/assets/Images/Sanctuary.png'),
          type:" ",
          Movie_Name1: "Sanctuary",
          Movie_Name2: " "
        },
        Img6:{
          Movie_Path: require('@/assets/Images/TalkToMe.jpg'),
          type:" ",
          Movie_Name1: "Talk To Me",
          Movie_Name2: " "
        },
        Img7:{
          Movie_Path: require('@/assets/Images/AboutMyFather.png'),
          type:"NEW",
          Movie_Name1: "About My Father",
          Movie_Name2: " "
        },
        Img8:{
          Movie_Path: require('@/assets/Images/Air.png'),
          type:" ",
          Movie_Name1: "Air",
          Movie_Name2: " "
        },
        Img9:{
          Movie_Path: require('@/assets/Images/AreYouThereGod.png'),
          type:"NEW",
          Movie_Name1: "Are You There God?",
          Movie_Name2: "It's Me, Margaret"
        },
        Img10:{
          Movie_Path: require('@/assets/Images/GuardiansOfTheGalaxy.png'),
          type:" ",
          Movie_Name1: "Guardians Of The Galaxy:",
          Movie_Name2: "Volume 3"
        },
        Img11:{
          Movie_Path: require('@/assets/Images/BigGeorgeForeman.png'),
          type:" ",
          Movie_Name1: "Big George Foreman",
          Movie_Name2: " "
        },
        Img12:{
          Movie_Path: require('@/assets/Images/BeauIsAfraid.jpg'),
          type:" ",
          Movie_Name1: "Beau Is Afraid",
          Movie_Name2: " "
        }
      }
    };
  },
  methods:{
    moveLeft()
    {
      this.left=true;
      this.right=false;
      if(this.currentIndex<Object.keys(this.images).length-1)
        this.currentIndex++;
      else  
        this.currentIndex=Object.keys(this.images).length-1;
      this.checkDivVisibility();
      this.click_sound.currentTime = 0;
      this.click_sound.play();
      let viewportWidth = window.innerWidth;
      let divElements=document.querySelector(".carousel-inner");
      let remValue = 0;
      let rootFontSize = parseFloat(getComputedStyle(document.documentElement).fontSize);
      this.scrollValue=0;
      if(viewportWidth>=768)
      {
        remValue=21.438;
        this.scrollValue=((remValue*rootFontSize)+20);
      }
      else
      {
          remValue=13.438;
          this.scrollValue=((remValue*rootFontSize)+20);
      }
      
      
      clearTimeout(this.scrollTimeout);
      setTimeout(()=>{
        if(!this.left)
          divElements.scrollLeft+=this.scrollValue;
      },500);
       
      console.log("Clicked");
    },
    moveRight()
    {
      this.left=false;
      this.right=true;
      this.click_sound.currentTime = 0;
      this.click_sound.play();
      let viewportWidth = window.innerWidth;
      let divElements=document.querySelector(".carousel-inner");
      this.remValue = 0;
      this.rootFontSize = parseFloat(getComputedStyle(document.documentElement).fontSize);
      this.scrollValue=0;
      if(viewportWidth>=768)
      {
        this.remValue=21.438;
        this.scrollValue=((this.remValue*this.rootFontSize)+20);
      }
      else
      {
          this.remValue=13.438;
          this.scrollValue=((this.remValue*this.rootFontSize)+20);
      }
  
      clearTimeout(this.scrollTimeout);
      setTimeout(()=>{
        if(this.currentIndex>0)
          this.currentIndex--;
        else
          this.currentIndex=0;
        this.checkDivVisibility();
        if(!this.right)
        divElements.scrollLeft-=this.scrollValue;
        
      },500);
      
      console.log("Clicked");
    },
    checkDivVisibility() 
    {
      const divs = document.querySelectorAll('#EachMovie');
      // console.log(divs);
      let divElements=document.querySelector(".carousel-inner");
      const targetDiv = document.querySelector(`[div-index="${this.currentIndex}"]`);
      console.log(targetDiv);
      if (this.isElementInViewport(targetDiv)) 
      {
        console.log('Target div is completely in viewport!');

        divs.forEach((div) => {
          console.log(this.currentIndex);
          const divIndex = parseInt(div.getAttribute('div-index'));
          if (divIndex === this.currentIndex)
          {
            div.classList.remove('scale-down');
          }
          else
          {
            div.classList.add('scale-down');
          }
        });
      } 
      else 
      if(targetDiv!=null)
      {
        if(this.left)
          divElements.scrollLeft+=this.scrollValue;
        else
          divElements.scrollLeft-=this.scrollValue;
        divs.forEach((div) => {
          console.log(this.currentIndex);
          const divIndex = parseInt(div.getAttribute('div-index'));
          if (divIndex === this.currentIndex)
          {
            div.classList.remove('scale-down');
          }
          else
          {
            div.classList.add('scale-down');
          }
        });
        console.log('Target div is not completely in viewport!');
      }
    },
    isElementInViewport(el) {
      const rect = el.getBoundingClientRect();
      return (
        rect.top >= 0 &&
        rect.left >= 0 &&
        rect.bottom <= (window.innerHeight || document.documentElement.clientHeight) &&
        rect.right <= (window.innerWidth || document.documentElement.clientWidth)
      );
    },
    moveDivLeft(){
      this.moveLeft(); 
    },
    moveDivRight(){
       this.moveRight();

    },
    handleKeyPress(event) 
    {
      console.log(`Key pressed: ${event.key}`);
      if(event.code=='ArrowLeft')
      {
        this.moveRight();
      }
      else
      if(event.code=='ArrowRight' || event.keyCode === 9)
      {
        this.moveLeft();
      }
    }
  }
}
</script>

<style>

*{
  background-color: black;
  scroll-behavior: smooth;
}



#main_heading
{
  font-size: 1.5rem;
  font-weight: 675;
  color: rgba(255, 255, 255, 1);
  letter-spacing: 0.106rem;
}

@media screen and (min-width: 768px) {
  #main
  {
    display: flex;
    flex-direction: column;
    justify-content: center; 
    height: 100vh;
  }
  #main_heading
  {
    font-size: 3rem;
    font-weight: 675;
    color: rgba(255, 255, 255, 1);
    letter-spacing: 0.106rem;
  }
  
}


.d-flex
{
  gap: 20px;
}

.carousel-inner
{
  overflow-x: scroll;
}

.carousel-inner::-webkit-scrollbar {
  visibility: hidden;
}

.scale-down
{
  transform: scale(0.7);
  transition: transform 0.5s ease-in;
}

</style>
