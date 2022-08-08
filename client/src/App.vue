<script>
import axios from "axios";
import Login from "./components/Login.vue";
import Button from "./components/Button.vue";
import Dashboard from "./components/Dasboard.vue";
import Header from "./components/Header.vue";
import Register from "./components/Register.vue";
import Sidebar from "./components/Sidebar.vue";
import TableProduct from "./components/TableProduct.vue";
import TableCategory from "./components/TableCategory.vue";
import TableHistory from "./components/TableHistory.vue";
import Form from "./components/Form.vue";
const baseUrl = "http://localhost:3000";
export default {
  name: "App",
  data() {
    return {
      isLogin: false,
      page: "login",
      user: {
        username: "",
        email: "",
        phoneNumber: "",
        address: "",
        role: "",
        password: "",
      },
      products: [],
      dataProductById: {},
      categories: [],
      histories: [],
    };
  },
  components: {
    Login,
    Sidebar,
    Register,
    Dashboard,
    Header,
    Button,
    TableProduct,
    TableCategory,
    TableHistory,
    Form,
  },
  methods: {
    pageChanger: function (pageName) {
      this.page = pageName;
      this.getAllHistories();
      this.getListCategory();
      this.getProducts();
    },
    handlerLogin: async function (userData) {
      try {
        let response = await axios.post(`${baseUrl}/users/login`, {
          email: userData.email,
          password: userData.password,
        });

        localStorage.setItem("accessToken", response.data.data.accessToken);
        localStorage.setItem("userId", response.data.data.userId);
        localStorage.setItem("email", response.data.data.email);
        localStorage.setItem("username", response.data.data.username);
        localStorage.setItem("role", response.data.data.role);

        this.isLogin = true;
        this.getListCategory();
        this.getProducts();
        this.page = "main";
        swal.fire({
          title: "Success!",
          text: "Succesfully login to our Page!",
          icon: "success",
        });
      } catch (err) {
        swal.fire({
          icon: "error",
          title: "Fail!",
          text: err.response.data.message[0],
        });
      }
    },
    registForm: async function (userData) {
      try {
        await axios.post(`${baseUrl}/users/register`, {
          email: userData.email,
          username: userData.username,
          phoneNumber: userData.phoneNumber,
          address: userData.address,
          password: userData.password,
        });
        this.page = "login";
        swal.fire({
          title: "Success!",
          text: "Succesfully register user!",
          icon: "success",
        });
      } catch (err) {
        swal.fire({
          icon: "error",
          title: "Fail!",
          text: err.response.data.message[0],
        });
      }
    },
    // Function for Logout
    logoutHandler: async function () {
      try {
        google.accounts.id.disableAutoSelect();
        google.accounts.id.revoke(this.email, (done) => {
          localStorage.clear();
          this.page = "login";
          this.isLogin = false;
          this.email = "";
          swal.fire({
            title: "Success!",
            text: "Succesfully logout from our system!",
            icon: "success",
          });
        });
        google.accounts.id.renderButton(
          document.getElementById("google-button"),
          { theme: "outline", size: "large", width: 1000 } // customization attributes
        );
      } catch (error) {
        swal.fire({
          title: "Fail!",
          text: "Test",
          icon: "error",
        });
      }
    },
    // Function For get All Product Data
    getProducts: async function () {
      try {
        let headers = {
          access_token: localStorage.getItem("accessToken"),
        };
        const response = await axios.get(`${baseUrl}/products`, { headers });
        this.products = response.data.product;
      } catch (err) {
        swal.fire({
          icon: "error",
          title: "Fail!",
          text: "Cannot Get Data Product",
        });
      }
    },
    // Function For create Product
    createProductHandler: async function (newProductData) {
      try {
        let newProduct = {
          name: newProductData.name,
          description: newProductData.description,
          imgUrl: newProductData.imgUrl,
          price: newProductData.price,
          categoryId: newProductData.categoryId,
          authorId: +localStorage.getItem("userId"),
        };
        let headers = {
          access_token: localStorage.getItem("accessToken"),
        };
        await axios.post(`${baseUrl}/products`, newProduct, {
          headers: headers,
        });

        this.page = "listProducts";
        this.getProducts();
        swal.fire({
          icon: "success",
          title: "Success!",
          text: "Succesfully add New Product!",
        });
      } catch (err) {
        swal.fire({
          icon: "error",
          title: "Fail!",
          text: err.response.data.message[0],
        });
      }
    },
    // Function For get ProductId
    editProductHandler: async function (productId) {
      try {
        let headers = {
          access_token: localStorage.getItem("accessToken"),
        };
        let response = await axios.get(`${baseUrl}/products/${productId}`, {
          headers,
        });
        this.dataProductById = response.data.data;
      } catch (error) {
        swal.fire({
          icon: "error",
          title: "Fail!",
          text: error.response.data.message[0],
        });
      }
    },
    // Function For Update Product
    updateProductHandler: async function (updatedProduct) {
      try {
        let id = this.dataProductById.id;
        let newUpdateProduct = {
          name: updatedProduct.name,
          description: updatedProduct.description,
          price: updatedProduct.price,
          imgUrl: updatedProduct.imgUrl,
          categoryId: updatedProduct.categoryId,
          authorId: +localStorage.getItem("userId"),
        };
        let headers = {
          access_token: localStorage.getItem("accessToken"),
        };
        await axios.put(`${baseUrl}/products/${id}`, newUpdateProduct, {
          headers,
        });
        this.page = "listProducts";
        this.getProducts();
        swal.fire({
          icon: "success",
          title: "Success!",
          text: "Succesfully update Product!",
        });
      } catch (err) {
        swal.fire({
          icon: "error",
          title: "Fail!",
          text: err.response.data.message[0],
        });
      }
    },
    // Function For Change Status
    statusChange: async function (newStatus, productId) {
      try {
        let headers = {
          access_token: localStorage.getItem("accessToken"),
        };
        await axios.patch(
          `${baseUrl}/products/${productId}`,
          { status: newStatus },
          {
            headers,
          }
        );

        swal.fire({
          icon: "success",
          title: "Success!",
          text: "Succesfully update Product status!",
        });
      } catch (err) {
        swal.fire({
          icon: "error",
          title: "Fail!",
          text: "Update Status Error",
        });
      }
    },
    // Function For Get All Category
    getListCategory: async function () {
      try {
        let headers = {
          access_token: localStorage.getItem("accessToken"),
        };
        let response = await axios.get(`${baseUrl}/categories`, {
          headers,
        });

        this.categories = response.data.data;
      } catch (err) {
        swal.fire({
          icon: "error",
          title: "Fail!",
          text: "Get Categories Error",
        });
      }
    },
    // Function For Get All History
    getAllHistories: async function () {
      try {
        let headers = {
          access_token: localStorage.getItem("accessToken"),
        };
        let response = await axios.get(`${baseUrl}/products/histories`, {
          headers,
        });

        this.histories = response.data.readHistory;
      } catch (err) {
        swal.fire({
          icon: "error",
          title: "Fail!",
          text: err.response.data.message[0],
        });
      }
    },

    handleCredentialResponse(response) {
      // console.log("Encoded JWT ID token: " + response.credential);
      axios({
        method: "POST",
        url: `${baseUrl}/users/google-login`,
        data: {
          credential: response.credential,
        },
      })
        .then((response) => {
          const { accessToken, email, username, role } = response.data;
          localStorage.setItem("accessToken", accessToken);
          localStorage.setItem("email", email);
          localStorage.setItem("username", username);
          localStorage.setItem("role", role);
          console.log(response.data, "ini respon");
          this.isLogin = true;
          this.getListCategory();
          this.getProducts();
          this.page = "main";
        })
        .catch((err) => {
          console.error(err, "Google sign in Error Nih !!");
        });
    },
  },
  mounted() {
    const cb = this.handleCredentialResponse;
    window.onload = function () {
      google.accounts.id.initialize({
        client_id:
          "317944751357-oek19ae5l2ih4i1b9mujgrqtm1muqkjm.apps.googleusercontent.com",
        callback: cb,
      });
      google.accounts.id.renderButton(
        document.getElementById("google-button"),
        { theme: "outline", size: "large", width: 1000 } // customization attributes
      );
      // google.accounts.id.prompt(); // also display the One Tap dialog
    };
  },
  // LifeCyle Function After create App
  created() {
    if (localStorage.getItem("accessToken")) {
      this.isLogin = true;
      this.user.username = localStorage.getItem("username");
      this.user.role = localStorage.getItem("role");
      this.user.email = localStorage.getItem("email");
      this.page = "main";
      this.getListCategory();
    } else {
      this.isLogin = false;
      this.page = "login";
    }
  },
  updated() {
    this.user.username = localStorage.getItem("username");
    this.user.role = localStorage.getItem("role");
    this.user.email = localStorage.getItem("email");
  },
};
</script>

<template>
  <div>
    <Login
      @login-user="handlerLogin"
      @display-page="pageChanger"
      v-if="page === 'login'"
    ></Login>
    <Register
      @registration-user="registForm"
      @display-page="pageChanger"
      v-else-if="page === 'registration'"
    ></Register>
    <div
      v-if="isLogin === true"
      class="bg-gray-100 dark:bg-gray-800 rounded-2xl overflow-hidden relative"
    >
      <div class="flex items-start justify-between">
        <Sidebar @display-page="pageChanger"></Sidebar>
        <div class="flex flex-col w-full pl-0 md:p-4 md:space-y-4">
          <Header @log-out="logoutHandler" :user="user"></Header>
          <Dashboard v-if="page === 'main'" :user="user"></Dashboard>
          <TableProduct
            v-if="page === 'listProducts'"
            v-bind:products="products"
            v-bind:categories="categories"
            @display-page="pageChanger"
            @change="statusChange"
            @edit-product="editProductHandler"
          ></TableProduct>
          <TableHistory
            v-if="page === 'listHistory'"
            v-bind:histories="histories"
          ></TableHistory>
          <TableCategory
            v-if="page === 'listCategory'"
            v-bind:categories="categories"
          ></TableCategory>
          <Form
            v-if="page === 'formAddProduct'"
            v-bind:categories="categories"
            @create-product="createProductHandler"
          ></Form>
          <Form
            v-if="page === 'editFormProduct'"
            v-bind:categories="categories"
            v-bind:products="dataProductById"
            @update-product="updateProductHandler"
          ></Form>
        </div>
      </div>
    </div>
  </div>
</template>
