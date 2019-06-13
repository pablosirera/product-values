<template>
  <!-- This styles and html are from https://codepen.io/jamesbarnett/pen/vlpkh -->
  <div class="rating">
    <input id="star5" type="radio" name="rating" value="5" />
    <label class="full" for="star5"></label>
    <input id="star4" type="radio" name="rating" value="4" />
    <label class="full" for="star4"></label>
    <input id="star3" type="radio" name="rating" value="3" />
    <label class="full" for="star3"></label>
    <input id="star2" type="radio" name="rating" value="2" />
    <label class="full" for="star2"></label>
    <input id="star1" type="radio" name="rating" value="1" />
    <label class="full" for="star1"></label>
  </div>
</template>

<script>
export default {
  name: 'Stars',
  props: {
    value: {
      type: String,
      default: '2'
    }
  }
}
</script>

<style lang="scss">
@import url('//netdna.bootstrapcdn.com/font-awesome/3.2.1/css/font-awesome.css');

.rating {
  border: none;
  float: left;
}

.rating > input {
  display: none;
}
.rating > label:before {
  margin: 5px;
  font-size: 1.25em;
  font-family: FontAwesome;
  display: inline-block;
  content: '\f005';
}

.rating > .half:before {
  content: '\f089';
  position: absolute;
}

.rating > label {
  color: #ddd;
  float: right;
}

/***** CSS Magic to Highlight Stars on Hover *****/

.rating > input:checked ~ label, /* show gold star when clicked */
.rating:not(:checked) > label:hover, /* hover current star */
.rating:not(:checked) > label:hover ~ label {
  color: #ffd700;
} /* hover previous stars in list */

.rating > input:checked + label:hover, /* hover current star when changing rating */
.rating > input:checked ~ label:hover,
.rating > label:hover ~ input:checked ~ label, /* lighten current selection */
.rating > input:checked ~ label:hover ~ label {
  color: #ffed85;
}
</style>
