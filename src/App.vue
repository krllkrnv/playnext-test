<template>
  <v-container class="product">
    <v-row class="product__row">
      <v-col class="product__col" cols="12" md="6">
        <v-carousel cycle :show-arrows="false" class="product__carousel">
          <v-carousel-item
            v-for="(image, index) in images"
            :key="index"
            :src="image"
            class="product__carousel-item"
          ></v-carousel-item>
        </v-carousel>
        <v-tabs v-model="tab" class="product__tabs">
          <v-tab value="description" class="product__tab">Описание</v-tab>
          <v-tab value="specs" class="product__tab">Характеристики</v-tab>
        </v-tabs>
        <v-window v-model="tab" class="product__window">
          <v-window-item value="description" class="product__window-item">
            <p
              v-html="product.description.replace(/\n/g, '<br><br>')"
              class="product__description"
            ></p>
          </v-window-item>
          <v-window-item value="specs" class="product__window-item">
            <v-table class="product__table">
              <tbody>
                <tr
                  v-for="(value, key) in product.specs"
                  :key="key"
                  class="product__spec"
                >
                  <td class="product__spec-key">
                    <strong>{{ key }}</strong>
                  </td>
                  <td class="product__spec-value">{{ value }}</td>
                </tr>
              </tbody>
            </v-table>
          </v-window-item>
        </v-window>
      </v-col>
      <v-col class="product__col" cols="12" md="6">
        <h1 class="product__name">{{ product.name }}</h1>
        <h2 class="product__price">{{ product.price }} ₽</h2>
        <v-form @submit.prevent="submitForm" class="product__form">
          <v-text-field
            v-model="form.name"
            label="Ваше имя"
            required
            class="product__input"
          ></v-text-field>
          <v-text-field
            v-model="form.phone"
            label="Телефон"
            required
            class="product__input"
          ></v-text-field>
          <v-btn
            :disabled="!form.name || !form.phone"
            type="submit"
            color="primary"
            class="product__btn"
            >Заказать сейчас</v-btn
          >
        </v-form>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
import { ref } from "vue";

const product = ref({
  name: '6.1" Смартфон Apple iPhone 15 128 ГБ черный',
  price: 74799,
  description: `Встречайте смартфон Apple iPhone 15. Он не оставит вас в беде благодаря экстренному оповещению через спутник и функцию определения аварии. Помощь придет в самый нужный момент.
Модель отличается стильным внешним видом. Непревзойденное сочетание цвета и долговечности: стекло и алюминий в едином дизайне. Корпус Apple iPhone 15 выполнен из 75% переработанного алюминия.
Чип A16 Bionic демонстрирует невероятную мощь, признанную экспертами. Заряда устройства хватает на весь день для всего, что вам по душе. Смотрите видео до 20 часов. Для подзарядки аккумулятора воспользуйтесь разъемом USB Type-C.
Основная камера 48 Мп с 2-кратным телеобъективом позволит делать снимки в высочайшем разрешении.`,
  specs: {
    Дисплей: '6.1" AMOLED',
    Разрешение: "2556x1179",
    "Операционная система": "iOS 17",
    Процессор: "A16 Bionic",
    "Оперативная память": "6 ГБ LPDDR5",
    "Встроенная память": "128/256/512 ГБ, без поддержки microSD",
    "Основная камера": "48 МП + 12 МП (ультраширокоугольная)",
    "Фронтальная камера": "12 МП с автофокусом",
    Аккумулятор: "3279 мА·ч, поддержка быстрой зарядки MagSafe (15 Вт)",
  },
});

const images = ref([
  "https://c.dns-shop.ru/thumb/st1/fit/0/0/b01f455e0db36429001e817cc9a08484/2258685cc32bbd96de406852bd9b2d94916029658cd6fa120a9f97a4bc0af297.jpg.webp",
  "https://c.dns-shop.ru/thumb/st1/fit/0/0/b500bdc0416222116480e78294783e71/be0cbf2360c7489de2559c39d58b08e0517a9546502a3bc859b4ee678c42427b.jpg.webp",
  "https://c.dns-shop.ru/thumb/st1/fit/0/0/43da8634f1206d6e21c727d2f4992f53/2a2217c04dc28db8403122239b91dc37b5da40828150349c06afa10ec99f1963.jpg.webp",
  "https://c.dns-shop.ru/thumb/st1/fit/0/0/d9419d3258573b0e2bea08b388ef3e7e/712f29edfb356bb1be9e872dc4b8cdc70be18a81182698eeae7b431083d8b009.jpg.webp",
  "https://c.dns-shop.ru/thumb/st4/fit/0/0/9ae6625d3e7b892a19e82976f397cc27/0618ce76feb9d36deefd8c81f404e2f30be58f754eeae668c91dad47a48f4eed.jpg.webp",
]);

const tab = ref("description");

const form = ref({
  name: "",
  phone: "",
});

const submitForm = () => {
  alert(
    `Заказ отправлен! Имя: ${form.value.name}, Телефон: ${form.value.phone}`
  );
};
</script>

<style scoped lang="scss">
.product {
  &__name {
    font-size: 24px;
  }
  &__price {
    margin-bottom: 22px;
  }
  &__window {
    padding: 16px;
    background-color: rgb(243, 243, 243);
    &-item {
      border-radius: 8px;
    }
  }
}
</style>
