<template>
  <v-app>
    <!-- <v-container > -->
    <br /><br />
    <v-container>
      <v-col cols="12" lg="8">
        <v-card max-width="100%">
          <h2 class="d-flex justify-center pt-8">Algorithm Search</h2>
          <v-container>
            <v-row>
              <v-col cols="2" xs="4">List</v-col>
              <v-col cols="8" xs="10">
                <v-text-field
                  v-model="numlist"
                  @keyup="input_num()"
                ></v-text-field>
              </v-col>
              <v-col cols="2"><v-btn @click="Clearlist" color="error">ลบค่า</v-btn></v-col>

            </v-row>
            <v-row>
              <v-col cols="2" xs="4">ค้นหา</v-col>
              <v-col cols="8" xs="10">
                <v-text-field v-model="Search_input"></v-text-field>
              </v-col>
              <v-col cols="2"><v-btn @click="Search_fn" color="warning">ค้นหา</v-btn></v-col>

            </v-row>
            <v-row>
              <v-col class="d-flex justify-center"> ประเภทการค้นหา </v-col>
            </v-row>
            <v-row>
              <v-col>
                <v-col ccols="8" xs="12" class="d-flex justify-center">
                  <v-select
                    v-model="condition_select"
                    :items="condition"
                    menu-props="auto"
                    selection
                  ></v-select>
                </v-col>
                     <v-col ccols="8" xs="12" class="d-flex justify-center">
             *** หมายเหต : เนื่องจากผมไม่เคยได้ยิน Algorithm Bubble Search ****
                </v-col>
              </v-col>
            </v-row>
            <v-row class="d-flex justify-center">
              <v-col cols="12">
                ผลลัพธ์
                <v-card max-width="100%" outlined>
                  <v-row>
                    <v-col class="d-flex justify-center pt-"
                      >List : {{ listvalue }}
                    </v-col>
                  </v-row>
                  <v-row class="d-flex justify-center">
                    <v-col class="d-flex justify-center"
                      >Search : {{ Search_input }}</v-col
                    >
                  </v-row>
                  <v-row class="d-flex justify-center">
                    <v-col class="d-flex justify-center">Result ::: </v-col>
                  </v-row>
                  <v-row
                    class="d-flex justify-center"
                    v-for="index in outputSearch"
                    :key="index"
                  >
                    <v-col class="d-flex justify-center" cols="12">{{
                      index
                    }}</v-col>
                  </v-row>
                </v-card>
              </v-col>
            </v-row>
           
          </v-container>
        </v-card>
      </v-col>
    </v-container>

    <!-- </v-container> -->
  </v-app>
</template>

<script>
export default {
  name: "Search_page",
  data() {
    return {
      numlist: "",
      condition: ["Linear Search", "Binary Search", "Bubble Search"],
      condition_select: "Linear Search",
      Search_input: "",
      outputSearch: "",
      listvalue: "",
    };
  },
  methods: {
    Clearlist() {
      this.numlist = "";
    },

    input_num() {
      if (this.numlist.length > 0) {
        this.numlist = this.numlist + ",";
      } else {
        console.log("Nothing here");
      }
    },

    Search_fn() {
      let result_search = [];
      var search_value = "";
      var value;
      search_value = this.numlist.split(",");
      search_value.pop();
      if (this.condition_select == "Linear Search") {
        this.listvalue = search_value;
        let index = 1;
        for (value of search_value) {
          if (value != this.Search_input) {
            result_search.push(
              "Round" + index + " :===>" + this.Search_input + "!=" + value
            );
          }
          if (value == this.Search_input) {
            result_search.push(
              "Round" +
                index +
                " :===>" +
                this.Search_input +
                " = " +
                value +
                "found !!"
            );
            break;
          }
          index++;
        }
        console.log(result_search);
      }
      if (this.condition_select == "Binary Search") {
        this.listvalue = search_value;
        let startindex = 0;
        console.log("startindex :" + startindex);
        let endindex = search_value.length - 1;
        console.log("endindex :" + endindex);

        while (startindex <= endindex) {
          let midindex = Math.floor((endindex + startindex) / 2);
          console.log((midindex = Math.floor((endindex + startindex) / 2)));

          var guess = search_value[midindex];
          console.log(guess);
          if (guess == this.Search_input) {
            result_search.push("Index : " + midindex + "found !!");
          }
          if (guess > this.Search_input) {
            endindex = midindex - 1;
          } else {
            startindex = midindex + 1;
          }
        }
      }
      if (this.condition_select == "Bubble Search") {
        search_value;
        var index = 1;
        var len = search_value.length;
        for (let i = 0; i < len; i++) {
          for (let j = 0; j < len - i - 1; j++) {
            console.log(len);
            if (search_value[j] > search_value[j + 1]) {
              if (search_value[i] === this.Search_input) {
                result_search.push(
                  "Round : " +
                    index +
                    "===>" +
                    search_value[i] +
                    "==" +
                    this.Search_input +
                    "found !!"
                );
                break;
              } else
                result_search.push(
                  "Round : " +
                    index +
                    "===>" +
                    search_value[i] +
                    "!=" +
                    this.Search_input +
                    "Not found !!"
                );
              let tmp = search_value[j];
              search_value[j] = search_value[j + 1];
              search_value[j + 1] = tmp;
            }
          }
          index++;
        }
        result_search.push("Sort : " + search_value);
      }

      this.outputSearch = result_search;
    },
  },
};
</script>