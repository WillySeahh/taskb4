<template>
  <div>
    <b-jumbotron style="background-color:#90ee90" header="CS3219 OTOT B4">
      <p>This front end web page is developed using Vue</p>
      <hr/>
      <h2>Marking Scheme</h2>
      <p> Demonstrate ability to interact with the API using the frontend (2 marks) </p>
      <p> Implementation of style e.g. using Bootstrap (1 mark) </p>
      <p> Willy Seah Wee Hung </p>
      <p> A0183766N </p>

      <hr/>
      <h4> You can use this web page to test the API calls of the deployed end points using Lambda
        of Task B3 </h4>
      <p>Scroll below to test the CRUD operations </p>
    </b-jumbotron>

    <b-card title="GET REQUEST" sub-title="Get quote(s) from backend">
      <b-card-body>
        <b-container fluid>
          <h4>Get All Quotes</h4>
          <b-button v-on:click="getAll" variant="success">
            Get All Quotes
          </b-button>
          <b-button v-on:click="clearAll" variant="danger"> Reset </b-button>
          <b-list-group style="margin-top: 15px">
            <b-list-group-item v-for="quote in quotes" :key="quote.id" variant="success">
              <h5>Title: {{ quote.title}}</h5>
              <h6>Author: {{ quote.author }}</h6>
              <h6>Description: {{ quote.description }}</h6>
              <h6>Id: {{ quote.id }}</h6>
            </b-list-group-item>
            <b-list-group-item v-if="getallmessage != ''" style="margin-top: 15px" variant="danger">
              <h5>{{ getallmessage }}</h5>
            </b-list-group-item>
          </b-list-group>
        </b-container>

        <hr/>


        <b-container fluid>
          <h4>Get single quote</h4>
          <b-form>
            <b-form-group id="getGroup" label-for="get-1">
              <b-form-input
                id="get-1"
                v-model="formid"
                placeholder="Enter quote's id"
              ></b-form-input>
            </b-form-group>
            <b-button v-on:click="getSingle" variant="success">
              Get The Quote
            </b-button>
            <b-button v-on:click="clearSingle" variant="danger">
              Reset
            </b-button>
          </b-form>
          <b-list-group-item v-if="title != ''" style="margin-top: 15px" variant="success">
            <h5>Title: {{ title }}</h5>
            <h6>Author: {{ author }}</h6>
            <h6>Description: {{ description }}</h6>
            <h6>Id: {{ id }}</h6>

          </b-list-group-item>
          <b-list-group-item v-if="getsinglemessage != ''" style="margin-top: 15px" variant="danger">
            <h5>{{ getsinglemessage }}</h5>
          </b-list-group-item>
        </b-container>
      </b-card-body>
    </b-card>

    <b-card title="POST REQUEST" sub-title="Upload new quote to backend">
      <b-card-body>
        <b-container fluid>
          <h4>Add new quote</h4>
          <b-form>
            <b-form-group id="post-group-1" label-for="post-1">
              <b-form-input
                id="post-1"
                v-model="newtitle"
                required
                placeholder="Enter the title of quote "
              ></b-form-input>
            </b-form-group>
            <b-form-group id="post-group-2" label-for="post-2">
              <b-form-input
                id="post-2"
                v-model="newauthor"
                required
                placeholder="Enter the author of quote "
              ></b-form-input>
            </b-form-group>
            <b-form-group id="post-group-3" label-for="post-3">
              <b-form-input
                id="post-3"
                v-model="newdescription"
                required
                placeholder="Enter the description of quote"
              ></b-form-input>
            </b-form-group>
            <b-button v-on:click="addNew" variant="success"> Submit </b-button>
            <b-button v-on:click="clearAdd" variant="danger"> Reset </b-button>
            <h4 style="color: green" v-if="postmessage != ''">
              {{ postmessage }}
            </h4>
          </b-form>
        </b-container>
      </b-card-body>
    </b-card>

    <b-card title="PUT REQUEST" sub-title="Update existing quote">
      <b-card-body>
        <b-container fluid>
          <h4>Update quote</h4>
          <b-form>
            <b-form-group id="put-group-1" label-for="put-1">
              <b-form-input
                id="put-1"
                v-model="updateid"
                required
                placeholder="Enter id"
              ></b-form-input>
            </b-form-group>
            <b-form-group id="put-group-2" label-for="put-2">
              <b-form-input
                id="put-2"
                v-model="updatetitle"
                required
                placeholder="Enter updated title"
              ></b-form-input>

            </b-form-group>
                        <b-form-group id="put-group-3" label-for="put-3">
              <b-form-input
                id="put-3"
                v-model="updateauthor"
                required
                placeholder="Enter updated author"
              ></b-form-input>
            </b-form-group>

            <b-form-group id="put-group-2" label-for="put-2">
              <b-form-input
                id="put-2"
                v-model="updatedescription"
                required
                placeholder="Enter updated description"
              ></b-form-input>
            </b-form-group>

            <b-button v-on:click="update" variant="success"> Update </b-button>
            <b-button v-on:click="clearUpdate" variant="danger">
              Reset
            </b-button>
            <h4 style="color: red" v-if="updatequotemessage != ''">{{ updatequotemessage }}</h4>
          </b-form>
        </b-container>
      </b-card-body>
    </b-card>

    <b-card title="DELETE REQUEST" sub-title="Delete the quote">
      <b-card-body>
        <b-container fluid>
          <h4>Delete a quote</h4>
          <b-form>
            <b-form-group id="del-group-1" label-for="del-1">
              <b-form-input
                id="del-1"
                v-model="delid"
                required
                placeholder="Enter quote's id"
              ></b-form-input>
            </b-form-group>
            <b-button v-on:click="deleteSingle" variant="success">
              Delete
            </b-button>
            <b-button v-on:click="clearDelSingle" variant="danger">
              Reset
            </b-button>
            <h4 style="color: red" v-if="deleteonemessage != ''">
              {{ deleteonemessage }}
            </h4>

          </b-form>
        </b-container>

        <hr class="my-4" />

        <b-container fluid>
          <h4>Delete all quote</h4>
          <b-button v-on:click="deleteAll" variant="danger">
            Delete All Quotes
          </b-button>
          <h4 style="color: red" v-if="deleteallmessage != ''" variant="success">
            {{ deleteallmessage }}
          </h4>
        </b-container>
      </b-card-body>
    </b-card>
  </div>
</template>


<script>
import axios from "axios";
export default {
  name: "Home",
  data() {
    return {
      quotes: [],
      id: "",
      author: "",
      getallmessage: "",
      getsinglemessage: "",
      postmessage: "",
      updatequotemessage: "",
      deleteonemessage: "",
      deleteallmessage: "",
      err: "",
      formid: "",
      newauthor: "",
      newtitle:"",
      newdescription: "",
      updateid: "",
      updatetitle: "",
      updatedescription: "",
      updateauthor: "",
      delid: "",
      title: "",
      description: "",
    };
  },
  methods: {
    getAll() {
      axios
        .get(
          "https://kv2wuhd9ll.execute-api.ap-southeast-1.amazonaws.com/dev/api/quotes/"
        )
        .then((res) => {
          
          if (res.data.length == 0) {
            this.getallmessage = "No quotes in the backend";
          } else {
            this.quotes = res.data;
          }
        })
        .catch((err) => {
          this.err = err.message;
        });
    },
    clearAll() {
      this.quotes = [];
      this.getallmessage = "";
    },
    getSingle() {
      if (this.formid == "") {
        this.getsinglemessage = "Please Enter the Id of the quote";
      } else {
      axios
        .get(
          "https://kv2wuhd9ll.execute-api.ap-southeast-1.amazonaws.com/dev/api/quotes/".concat(
            this.formid
          )
        )
      .then((res) => {
          this.author = "";
          this.id = "";
          this.getsinglemessage = "";
          this.description = "";
          if (res.data != []) {
            this.title = res.data.title;
            this.author = res.data.author;
            this.description = res.data.description;
            this.id = res.data.id;
            this.formid = "";
          } else {
            this.getsinglemessage = "This quote not found!";
          }
        })
        .catch((err) => {
          this.err = err.message;
        });
    }},
    clearSingle() {
      this.title = "";
      this.author = "";
      this.id = "";
      this.getsinglemessage = "";
      this.formid = "";
    },


    addNew() {
    if (this.newtitle == "" || this.newauthor == "" || this.newdescription == "") {
        this.postmessage = "Please Enter title and author and description";
    }else{
      const data = {
        title: this.newtitle,
        author: this.newauthor,
        description: this.newdescription,
      };
      axios
        .post(
          "https://kv2wuhd9ll.execute-api.ap-southeast-1.amazonaws.com/dev/api/quotes/",
          data
        )
        .then((res) => {
          if (res.data.id != "") {
            this.postmessage = "Added Successfully";
            this.title = "";
            this.description = "";
            this.author = "";
          }
        })
        .catch((err) => {
          this.err = err.message;
        });
    }},
    clearAdd() {
      this.postmessage = "";
        this.newtitle = "";
        this.newdescription = "";
        this.newauthor = "";
    },

  //Update method
    update() {
      if (this.updateid == "") {
        this.updatequotemessage = "Please Enter the Id of the quote";
      } else {
        const data = {
          title : this.updatetitle,
          description: this.updatedescription,
          author: this.updateauthor,
        };
        axios
          .put(
            "https://kv2wuhd9ll.execute-api.ap-southeast-1.amazonaws.com/dev/api/quotes/".concat(
              this.updateid
            ),
            data
          )
          .then((res) => {
            if (res.data.status == "success") {
              this.updateid = "";
              this.updatedescription = "";
              this.updateauthor = "";
              this.updatetitle;
              this.updatequotemessage = "Updated Successfully";
            } else {
              this.updatequotemessage = "Update Quote Failed";
            }
          })
          .catch((err) => {
            this.err = err.message;
          });
      }
    },
    clearUpdate() {
      this.updateid = "";
      this.updatedescription = "";
      this.updateauthor = "";
      this.updatetitle = "",
      this.updatequotemessage = "";
    },

    //Delete quote
    deleteSingle() {
      if (this.delid == "") {
        this.deleteonemessage = "Please Enter the Id";
      } else {
        axios
          .delete(
            "https://kv2wuhd9ll.execute-api.ap-southeast-1.amazonaws.com/dev/api/quotes/".concat(
              this.delid
            )
          )
          .then((res) => {
            if (res.data.message == "Quote was deleted successfully!") {
              
              this.deleteonemessage = "Deleted Successfully"
              this.delid = "";
            } else {
              this.deleteonemessage = "Delete Failed";
            }
          })
          .catch((err) => {
            this.err = err.message;
          });
      }
    },
    clearDelSingle() {
      this.delid = "";
      this.deleteonemessage = "";
    },

    deleteAll() {
      axios
        .delete(
          "https://kv2wuhd9ll.execute-api.ap-southeast-1.amazonaws.com/dev/api/quotes/"
        )
        .then((res) => {
          if (res.data.id != "") {
            this.deleteallmessage = "Delete successfully";
          }
        })
        .catch((err) => {
          this.err = err.message;
        });
    },
  },
};
</script>