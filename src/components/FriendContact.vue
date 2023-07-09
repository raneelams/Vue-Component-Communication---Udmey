<template>
  <li>
    <h2>{{ name }} {{ isFavorite ? '(Favorite)' : '' }}</h2>
    <button @click="toggleFavorite">Toggle Favorite</button> </br>
    <button @click="toggleDetails">
      {{ detailsAreVisible ? 'Hide' : 'Show' }} Details
    </button>
    <ul v-if="detailsAreVisible">
      <li>
        <strong>Phone:</strong>
        {{ phoneNumber }}
      </li>
      <li>
        <strong>Email:</strong>
        {{ emailAddress }}
      </li>
    </ul> </br>
    <button @click="$emit('delete', id)"> Delete Friend </button>
  </li>
</template>

<script>
export default {
  // props: ['name', 'phoneNumber', 'emailAddress', 'isFavorite'], // or props can use as like objects also in below
  props: {
    id: {
      type: String,
      required : true
    },
    name : {
      type : String,
      required : true
    },
    phoneNumber : {
      type : String,
      required : true
    },
    emailAddress : {
      type : String,
      required : true
    },
    isFavorite : {
      type : Boolean,
      required : false,
      default : false,
      // validator: function (value) {
      //   return value === "1" || value === "0";
      // }
    },
  },  
  emits:['toggleFavorite', 'delete'], 
  // emits are used as custom method names in parent component.
  //emtis can also write as functions in like below.
  // emits:{
  //   'toggleFavorite' : function(id) {
  //     if(id) {
  //       return true
  //     } else {
  //       return false;
  //       console.log('id is missing')
  //     }
  //   }
  // }
  data() {
    return {
      detailsAreVisible: false
    };
  },
  methods: {
    toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible;
    },
    toggleFavorite() {
      this.$emit('toggle-favorite', this.id );
    },
    // deleteFriend() {   //We can use this funciton directly on template to delete the friends item
    //   this.$emit('delete ')
    // }
  },
};
</script>
