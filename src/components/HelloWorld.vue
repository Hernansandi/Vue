<template>
  <div>
    <div v-if="currentView === 'men'">
        <div class="back bck-men">
          <div class="container">
            <img src="../assets/men.jpg" alt="men's clothing">
            <div class="detail">
              <h1 class="cl-men">Mens Casual Slim Fit</h1>
              <div class="flex">
                <div class="nameproduct">men's clothing</div>
                <div class="flex rating">
                  <div class="rating-nilai">2.9/5</div>
                  <div class="rating-circle solid-men rating-men"></div>
                  <div class="rating-circle solid-men rating-men"></div>
                  <div class="rating-circle solid-men rating-men"></div>
                  <div class="rating-circle rating-men"></div>
                  <div class="rating-circle rating-men"></div>
                </div>
              </div>
              <hr>
              <div class="desc">
                great outerwear jackets for Spring/Autumn/Winter, suitable for many occasions, such as working, hiking, camping, mountain/rock climbing, cycling, traveling or other outdoors. Good gift choice for you or your family member. A warm hearted love to Father, husband or son in this thanksgiving or Christmas Day.
              </div>
              <hr>
              <div class="price cl-men">$29.95</div>
              <div class="flex">
                <button class="btn btn-solid-men btn-men">Buy now</button>
                <button @click="fetchProducts" class="btn btn-men">Next produk</button>
              </div>
            </div>
          </div>
        </div>
    </div> 
    <div v-if="currentView === 'women'">
      <div class="back bck-women">
        <div class="container">
          <img src="../assets/women.jpg" alt="women's clothing">
          <div class="detail">
            <h1 class="cl-women">Lock and Love Women's Removable Hooded Faux Leather Moto Biker Jacket</h1>
            <div class="flex">
              <div class="nameproduct cl-women">women's clothing</div>
              <div class="flex rating">
                <div class="rating-nilai">2.9/5</div>
                <div class="rating-circle solid-women rating-women"></div>
                <div class="rating-circle solid-women rating-women"></div>
                <div class="rating-circle solid-women rating-women"></div>
                <div class="rating-circle rating-women"></div>
                <div class="rating-circle rating-women"></div>
              </div>
            </div>
            <hr>
            <div class="desc">
              100% POLYURETHANE(shell) 100% POLYESTER(lining) 75% POLYESTER 25% COTTON (SWEATER), Faux leather material for style and comfort / 2 pockets of front, 2-For-One Hooded denim style faux leather jacket, Button detail on waist / Detail stitching at sides, HAND WASH ONLY / DO NOT BLEACH / LINE DRY / DO NOT IRON
            </div>
            <hr>
            <div class="price cl-women">$29.95</div>
            <div class="flex">
              <button class="btn btn-solid-women btn-women">Buy now</button>
              <button @click="fetchProducts" class="btn btn-women">Next produk</button>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div v-if="currentView === 'unavailable'">
      <div class="back bck-un">
        <div class="container cont-un">
            <div class="center detail">
              <div class="desc">
                This product is unavailable to show
              </div>
              <button @click="fetchProducts" class="btn" >Next produk</button>
            </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'HelloWorld',
  data() {
    return {
      currentView: 'unavailable', // Default view
      product: {},
      currentIndex: 4,
    };
  },
  methods: {
    async fetchProducts() {
      try {
        const response = await axios.get('https://fakestoreapi.com/products/' + this.currentIndex);
        const product = response.data;

        if (product.category === "women's clothing") {
          this.currentView = 'women'; // Tampilan Women
        } else if (product.category === "men's clothing") {
          this.currentView = 'men'; // Tampilan Men
        } else {
          this.currentView = 'unavailable'; // Tampilan Unavailable
        }

        this.product = product;
        this.incrementIndex();
      } catch (error) {
        console.error('Error fetching product:', error);
      }
    },
    incrementIndex() {
      this.currentIndex = this.currentIndex < 20 ? this.currentIndex + 1 : 1;
    },
  },
};
</script>

<style scoped>
.back {
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 60vh;
  font-family: Arial, Helvetica, sans-serif;
}

.women{
  background-color: #FDE2FF; /* Atur latar belakang women menjadi pink */
  color: #720060;
}
.bck-men {
  background-color: #D6E6FF;
}

.bck-women {
  background-color: #FDE2FF;
}

.bck-un{
  background-color: #D8D7D7;
}
.cl-men{
  color: #002772;
}

.cl-women{
  color: #720060;
}
.bg-men{
  background-color: #002772;
}
.bg-women{
  background-color: #720060;
}

.container{
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: absolute;
  position: absolute;
  width: 60em;
  top : 5em;
  left : 8em;
  background-color: #fff;
  padding: 2.5em 2.5em;
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 0.75em;
  backdrop-filter: blur(1em);
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
}

.cont-un{
  background-image: url('../assets/unvailable.jpg');
  background-size: contain;
  background-position: center;
  background-repeat: no-repeat;
  height: 300px;
}

.center{
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  flex-direction: column;
}

.container img{
  height: 20em;
  max-width: 100%;
  max-height: 100%;
  margin-right: 5em;
}

h1{
  font-size: 24px;
  font-weight: 600;
  line-height: 33.89px;

}

.flex{
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nameproduct{
  color: #3F3F3F;
  font-size: 14px;
  font-weight: 400;
  line-height: 21.78px;
}

.rating{
  color: #3F3F3F;
  font-size: 14px;
  font-weight: 400;
  line-height: 21.78px;
}

.rating-nilai{
  margin-right: 0.5em;
}
.rating-circle{
  width: 14px;
  height: 14px;
  border-radius: 50%;
  margin: 0.1em;
}

.rating-men{
  border: 1px solid #002772;
}

.rating-women{
  border: 1px solid #720060;
}

.solid-men{
  background-color: #002772;
}

.solid-women{
  background-color: #720060;
}

.desc{
  font-weight: 400;
  font-size: 16px;
  line-height: 24.2px;
  margin: 1em 0 1.5em 0;
}

.price{
  font-weight: 600;
  font-size: 22px;
  line-height: 33.89px;
  margin-bottom: 0.15em;
}

.btn{
  width: 45%;
  background-color: #fff;
  outline: none;
  border-radius: 4px;
  padding: 0.5em 1em;
  font-size: 16px;
}

.btn-men{
  border: 3px solid #002772;
  color: #002772;
}
.btn-women{
  border: 3px solid #720060;
  color: #720060;
}
.btn-solid-men{
  background-color: #002772;
  color: #fff;
}

.btn-solid-women{
  background-color: #720060;
  color: #fff;
}
</style>
