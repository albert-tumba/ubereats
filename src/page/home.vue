<template>
  <div class="header">
    <i class="fas fa-bars"></i>
    <img
      src="https://d3i4yxtzktqr9n.cloudfront.net/web-eats-v2/ee037401cb5d31b23cf780808ee4ec1f.svg"
      class="logo-header"
    />
    <a class="position-button">
      <i class="fas fa-map-marker-alt"></i>
      <div class="city">Chelles</div>
      <div>•</div>
      <div class="time">Maintenant</div>
      <div></div>
    </a>
    <div class="input-search">
      <i class="fas fa-search"></i>
      <input type="text" placeholder="De quoi avez-vous envie ?" />
    </div>
  </div>

  <!--<div class="banner"></div>-->
  <div class="home-body">
    <RestaurantRow
      v-for="(data, i) in data_restaurant"
      :key="i"
      :three_restaurant="data"
    />
  </div>

  <div class="footer">
    <div class="frame">
      <div class="upper-frame">
        <div class="box-1">
          <img
            src="https://d3i4yxtzktqr9n.cloudfront.net/web-eats-v2/c266ad32e5e88af804b3a1b6b60098f9.svg"
            class="logo-footer"
          />
          <div class="logos-app">
            <a
              href="https://apps.apple.com/us/app/uber-eats-food-delivery/id1058959277"
            >
              <img
                src="https://d3i4yxtzktqr9n.cloudfront.net/web-eats-v2/fabed2f9a81147a5270fdd54b8b67db9.svg"
                class="app-store"
              />
            </a>
            <a
              href="https://play.google.com/store/apps/details?id=com.ubercab.eats"
            >
              <img
                src="https://d3i4yxtzktqr9n.cloudfront.net/web-eats-v2/159904ff42f507df7927bb232fe56efa.png"
                class="google-play"
              />
            </a>
          </div>
        </div>
        <div class="box-2">
          <a href="#" class="title-footer-section"> À propos d'UberEats </a>
          <ul>
            <li><a href="#"> Consulter notre blog </a></li>
            <li><a href="#"> Créer un compte professionel </a></li>
            <li><a href="#"> Ajoutez votre restaurant </a></li>
            <li><a href="#"> Devenez coursier-partenaire </a></li>
          </ul>
        </div>
        <div class="box-3">
          <a href="#" class="title-footer-section"> Obtenir de l'aide </a>
          <ul>
            <li><a href="#"> Affichez toutes les villes </a></li>
            <li><a href="#"> Tous les pays </a></li>
            <li><a href="#"> Restaurants à proximité </a></li>
            <li><a href="#"> Économisez sur votre première commande. </a></li>
            <li>
              <i class="fas fa-language"></i>
              <a href="#"> Français </a>
            </li>
          </ul>
        </div>
      </div>
      <hr class="separate-line" />
      <div class="bottom-frame">
        <div class="social-links">
          <li>
            <a href="#"><i class="fab fa-facebook-square"></i></a>
          </li>
          <li>
            <a href="#"><i class="fab fa-twitter"></i></a>
          </li>
          <li>
            <a href="#"><i class="fab fa-instagram"></i></a>
          </li>
        </div>
        <div class="bottom-category">
          <li>
            <a href="#"> Politique de confidentialité </a>
          </li>
          <li>
            <a href="#"> Conditions </a>
          </li>
          <li>
            <a href="#"> Tarifs </a>
          </li>
        </div>
      </div>
      <div class="bottom-line">
        <h3>
          Ce site est protégé par reCAPTCHA. Par ailleurs, la Politique de
          confidentialité et les Conditions d'utilisation de Google
          s'appliquent. © 2021 Albert Technologies lol
        </h3>
      </div>
    </div>
  </div>
</template>

<script>
//IMPORT
import BDD from "../BDD.js";
import { onMounted, ref } from "vue";
//COMPONENTS
import RestaurantRow from "../components/RestaurantRow.vue";

export default {
  name: "Home",
  components: {
    RestaurantRow,
  },
  setup() {
    class Restaurant {
      constructor(name, note, image, drive_time, delivery, price) {
        this.name = name;
        this.note = note;
        this.image = image;
        this.drive_time = drive_time;
        this.delivery = delivery;
        this.price = price;
      }
    }

    let data_restaurant = ref([]);

    const makeDataRestaurant = () => {
      let three_restaurant = [];

      for (const restaurant of BDD) {
        const new_restaurant = new Restaurant(
          restaurant.name,
          restaurant.note,
          restaurant.image,
          restaurant.drive_time,
          restaurant.delivery,
          restaurant.price,
        );

        if (three_restaurant.length === 2) {
          three_restaurant.push(new_restaurant);
          data_restaurant.value.push(three_restaurant);
          three_restaurant = [];
        } else {
          three_restaurant.push(new_restaurant);
        }
      }
    };

    onMounted(makeDataRestaurant);

    return {
      data_restaurant,
    };
  },
};
</script>

<style lang="scss">
.header {
  padding: 0px 40px;
  height: 96px;
  display: flex;
  align-items: center;
  justify-content: space-between;

  .fa-bars {
    font-size: 20px;
    color: black;
  }
  img {
    width: 146px;
    height: 24px;
  }
  .position-button {
    padding: 0px 14px;
    height: 48px;
    background: #eeeeee;
    border-radius: 500px;
    font-size: 15px;
    font-weight: bold;
    display: flex;
    align-items: center;
    justify-content: center;

    .fa-map-marker-alt {
      line-height: 1;
      font-size: 14px;
      height: 24px;
      overflow: hidden;
      margin-right: 9px;
      margin-top: 8px;
    }
    .city {
      text-overflow: ellipsis;
      white-space: nowrap;
      overflow: hidden;
      cursor: pointer;
      margin-right: 5px;
    }
    .time {
      white-space: nowrap;
      cursor: pointer;
      margin-left: 5px;
    }
  }
  .input-search {
    background-color: #f6f6f6;
    height: 50px;
    width: 832px;
    padding-left: 19px;
    box-shadow: inset 0px -1px 0px #e2e2e2;

    .fa-search {
      margin-right: 15px;
    }

    input {
      background-color: #f6f6f6;
      border: none;
      outline: none;
      margin-top: 15px;
      width: 185px;
    }
  }
}

//.banner {
//  height: 200px;
//  width: 100%;
//  background-image: url("../../public/banner-Ubereats.png");
//  background-size: cover;
//  background-position: center center;
// }
.home-body {
  padding: 0px 40px;
}

.footer {
  margin-top: 80px;
  padding: 72px 0px 88px;
  background-color: #000000;
  .frame {
    padding: 0px 40px;
    margin: 0 auto;
    min-width: 1024px;
    max-width: 1920px;
    box-sizing: border-box;
    .upper-frame {
      display: flex;
      .box-1 {
        display: flex;
        align-items: flex-start;
        flex: 2;
        justify-content: space-between;
        flex-direction: column;
        .logo-footer {
          margin-bottom: 64px;
          width: auto;
          height: 24px;
        }
        .app-store {
          height: 40px;
          margin-right: 16px;
        }
        .google-play {
          height: 40px;
        }
      }
      .box-2,
      .box-3 {
        display: flex;
        flex-direction: column;
        flex: 1;
        .title-footer-section {
          line-height: 20px;
          margin-bottom: 24px;
          font-size: 16px;
          font-weight: bold;
        }
        a {
          color: #ffffff;
          text-decoration: none;
          line-height: 24px;
        }
        a:hover {
          text-decoration: underline;
        }
        ul {
          padding: 0;
          margin: 0;
          list-style: none;
        }
        li {
          display: block;
          margin-bottom: 16px;
        }
        .fa-language {
          color: white;
          margin-right: 3px;
        }
      }
    }
    .separate-line {
      margin: 40px 0;
      background-color: #f6f6f6;
      border: none;
      height: 1px;
    }
    .bottom-frame {
      display: flex;
      justify-content: space-between;

      .social-links {
        display: flex;
        flex-direction: row;
        font-size: 18px;
        margin-left: -23px;
        i {
          color: white;
        }
      }
      .bottom-category {
        display: flex;
        flex-direction: row;

        a {
          color: white;
          text-decoration: none;
        }
      }
    }
    .bottom-line {
      color: white;
      margin-top: 10px;
      font-size: 13px;
      display: flex;
      flex-direction: row-reverse;
    }
  }
}
</style>
