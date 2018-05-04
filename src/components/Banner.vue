<template>
<div class="carousel">
   <h3 style="float: left">Top activities around you:</h3>
<carousel :per-page="4" :paginationPadding="2">
    <slide v-for="(place,index) in places" :key="index">
      <div class="casing">
        <div class="thumbnail">
          <img :src="place.image" alt="" style="height: 150px; width:300px">
          <a :href="place.url" target="_blank" class="middle">
            <p class="des">{{place.des}}</p>
            <div class="button">Book Now</div>
          </a>
        </div>
        <div class="caption">
          <h4>{{place.title}}</h4>
          
        </div>
    </div>
    </slide>
  </carousel>
</div>
  
</template>

<script>
import { Carousel, Slide } from 'vue-carousel';
import axios from 'axios';
export default {
  name: 'Banner',
  components: {
    Carousel,
    Slide
  },
  props: {
    msg: String
  },
  data: function() {
    return {
      mockData: [
        {
          title: 'Blue Mountains Day Tour',
          des:
            'No journey to Australia could be complete without exploring the tranquil beauty of the Blue Mountains.',
          url: 'https://bluemountainstoursydney.com.au/',
          image:
            'https://bluemountainstoursydney.com.au/wp-content/uploads/2017/12/Blue-Mountains-Tours-Three-Sisters.jpg'
        },
        {
          title: 'Manly Surf Schools',
          des: 'Experience the Australian Beach!',
          url: 'https://manlysurfschool.com/',
          image: 'https://manlysurfschool.com/wp-content/uploads/unknown.jpg'
        },
        {
          title: 'SEA LIFE Sydney Aquarium',
          des:
            'One of Sydney’s premier attractions, SEA LIFE Aquarium at Darling Harbour.',
          url: 'https://www.sydneyaquarium.com.au/',
          image:
            'https://www.darlingharbour.com//media/2783/sea_life_penguins_thumbnail.jpg'
        },
        {
          title: 'Sydney Harbour Bridge Climb',
          des:
            'Climbing the Sydney Harbour Bridge is exhilarating – and an unforgettable experience, too.',
          url: 'https://www.bridgeclimb.com/',
          image:
            'https://www.bridgeclimb.com/wp-content/uploads/2014/04/The-Experience-featured-image-1-800x741.jpg'
        },
        {
          title: 'Rocks Walking Tour',
          des: '90-minute walking tour of The Rocks, in Sydney.',
          url: 'http://www.rockswalkingtours.com.au/',
          image:
            'https://media-cdn.tripadvisor.com/media/photo-s/0d/f5/6d/9b/the-rocks-walking-tour.jpg'
        },
        {
          title: 'Oz Jet Boating',
          des:
            'We spin, splash, fishtail, and dash around all of the iconic sights Sydney Harbour.',
          url: 'https://www.ozjetboating.com.au/',
          image:
            'https://scontent.cdninstagram.com/vp/9df68e8e1952563c1527533a2b407f69/5B93713D/t51.2885-15/s640x640/sh0.08/e35/30830359_343867989351186_8633288855174250496_n.jpg'
        }
      ]
    };
  },
  created() {
    axios
      .get(`http://localhost:3001`)
      .then(response => {
        // JSON responses are automatically parsed.
        this.places = response.data;
      })
      .catch(e => {
        this.places = mockData;
      });
  }
};
</script>
<style scoped>
.carousel {
  background: #fff;
  padding: 10px 20px 20px 15px;
  position: fixed;
  bottom: 0;
  z-index: 999;
  border-top: 1px solid #ccc;
}
.casing {
  margin: 0 20px;
}
.middle {
  transition: 0.5s ease;
  opacity: 0;
  position: absolute;
  top: 50%;
  left: 50%;
  width: 70%;
  transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  text-align: center;
}
.button {
  background-color: #4caf50;
  color: white;
  font-size: 16px;
  padding: 10px 20px;
}
.des {
  color: black;
  text-align: justify;
  font-weight: 600;
  font-size: 14px;
}
.thumbnail {
  position: relative;
}
.thumbnail:hover img {
  opacity: 0.2;
}
.thumbnail:hover .middle {
  opacity: 1;
}
</style>
