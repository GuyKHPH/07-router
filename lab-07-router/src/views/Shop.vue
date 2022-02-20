/* eslint-disable no-redeclare */
<template>
  <v-container>
    <h1 class="text-center green--text">JUCCI Shop</h1>
    <v-container>
      <v-container class="d-flex flex-wrap">
        <v-card
          class="mx-auto mb-5"
          max-width="400"
          v-for="product in productList"
          :key="product.id"
        >
          <v-container class="d-flex justify-center">
            <v-img height="200px" width="400px" :src="product.image"> </v-img>
          </v-container>
          <v-card-title>
            <p id="pdtitle">{{ product.title }}</p>
          </v-card-title>
          <v-card-subtitle class="pb-0">
            <p id="pdid">No. {{ product.id }}</p>
          </v-card-subtitle>
          <v-card-text class="text--primary" id="detailshop">
            <div>
              <h3>{{ product.category }}</h3>
            </div>
            <br />
            <div>
              <p>Price {{ product.price }} $</p>
            </div>
          </v-card-text>

          <v-card-actions class="d-flex justify-center">
            <v-btn color="green" text @click="addCart(product)"> add </v-btn>

            <v-btn
              color="blue"
              text
              :to="{
                name: 'productdetail',
                params: {
                  id: product.id,
                  description: product.description,
                  title: product.title,
                  image: product.image,
                },
              }"
            >
              Detail
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-container>
      <v-container>
        <h2 class="text-center">Cart</h2>
        <h3 class="text-center">Total {{ total() }} $</h3>
        <v-simple-table>
          <template v-slot:default>
            <thead>
              <tr>
                <th class="text-left">Picture</th>
                <th class="text-left">Name</th>
                <th class="text-left">Price</th>
                <th class="text-left">Quantity</th>
                <th class="text-left">Total</th>
                <th class="text-left">Remove</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="item in carts" :key="item.id">
                <td>
                  <img :src="item.image" width="150px" height="150px" />
                </td>
                <td>{{ item.name }}</td>
                <td>{{ item.price }}</td>
                <td>{{ item.qty }}</td>
                <td>{{ item.total }}</td>
                <td><v-btn @click="deleteitem(i)">remove</v-btn></td>
              </tr>
            </tbody>
          </template>
        </v-simple-table>
      </v-container>
    </v-container>

    <router-view :key="$route.path"></router-view>
  </v-container>
</template>

<script>
export default {
  name: "Shop",
  data() {
    return {
      carts: [],
      pro1: 0,
      pro2: 0,
      pro3: 0,
      productList: [
        {
          id: 1,
          title: "Fjallraven - Foldsack No. 1 Backpack, Fits 15 Laptops",
          price: 109.95,
          description:
            "Your perfect pack for everyday use and walks in the forest. Stash your laptop (up to 15 inches) in the padded sleeve, your everyday",
          category: "men's clothing",
          image: "https://fakestoreapi.com/img/81fPKd-2AYL._AC_SL1500_.jpg",
          rating: {
            rate: 3.9,
            count: 120,
          },
        },
        {
          id: 2,
          title: "Mens Casual Premium Slim Fit T-Shirts ",
          price: 22.3,
          description:
            "Slim-fitting style, contrast raglan long sleeve, three-button henley placket, light weight & soft fabric for breathable and comfortable wearing. And Solid stitched shirts with round neck made for durability and a great fit for casual fashion wear and diehard baseball fans. The Henley style round neckline includes a three-button placket.",
          category: "men's clothing",
          image:
            "https://fakestoreapi.com/img/71-3HjGNDUL._AC_SY879._SX._UX._SY._UY_.jpg",
          rating: {
            rate: 4.1,
            count: 259,
          },
        },
        {
          id: 3,
          title: "Mens Cotton Jacket",
          price: 55.99,
          description:
            "great outerwear jackets for Spring/Autumn/Winter, suitable for many occasions, such as working, hiking, camping, mountain/rock climbing, cycling, traveling or other outdoors. Good gift choice for you or your family member. A warm hearted love to Father, husband or son in this thanksgiving or Christmas Day.",
          category: "men's clothing",
          image: "https://fakestoreapi.com/img/71li-ujtlUL._AC_UX679_.jpg",
          rating: {
            rate: 4.7,
            count: 500,
          },
        },
      ],
    };
  },
  methods: {
    addCart: function (product) {
      if (product.id == 1) {
        this.pro1 += 1;
        if (this.pro1 <= 1) {
          this.pushData(product);
        } else {
          var found = this.findindex(product);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      }
      if (product.id == 2) {
        this.pro2 += 1;
        if (this.pro2 <= 1) {
          this.pushData(product);
        } else {
          // eslint-disable-next-line no-redeclare
          var found = this.findindex(product);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      }
      if (product.id == 3) {
        this.pro3 += 1;
        if (this.pro3 <= 1) {
          this.pushData(product);
        } else {
          // eslint-disable-next-line no-redeclare
          var found = this.findindex(product);
          this.carts[found].qty += 1;
          this.carts[found].total =
            this.carts[found].qty * this.carts[found].price;
        }
      }
    },

    pushData(product) {
      this.carts.push({
        id: product.id,
        name: product.title,
        price: product.price,
        image: product.image,
        qty: 1,
        total: product.price,
      });
    },
    findindex: function (product) {
      for (var i = 0; i < this.carts.length; i++) {
        if (this.carts[i].id == product.id) {
          return i;
        }
      }
      return -1;
    },
    deleteitem(i) {
      this.carts.splice(i, 1);
    },
    total: function () {
      var sum = 0;
      this.carts.forEach(function (item) {
        sum += item.total;
      });
      return sum;
    },
  },
};
</script>

<style>
* {
  font-family: sans-serif;
}
#pdtitle {
  font-size: 22px;
  font-weight: bold;
}
#pdid {
  font-size: 18px;
}
</style>
