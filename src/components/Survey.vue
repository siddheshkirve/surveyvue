<template>
  <div class="container">
    <survey :survey="survey">sdgs</survey>
    <v-btn block outlined color="primary" @click="submitData">Submit</v-btn>
    <vuetify-datatable
      v-if="posts.length != 0"
      :posts="posts"
    ></vuetify-datatable>
  </div>
</template>
<script>
import * as SurveyVue from "survey-vue";
import vuetifyDatatable from "./VuetifyDatatable.vue";
import "bootstrap/dist/css/bootstrap.css";

var Survey = SurveyVue.Survey;

export default {
  components: {
    Survey,
    vuetifyDatatable
  },
  data() {
    var json = {
      showQuestionNumbers: "off",

      elements: [
        {
          type: "paneldynamic",
          name: "items",
          title: "Product data Data",
          keyName: "name",

          // templateTitle: "item No:{panelIndex}",

          templateElements: [
            {
              type: "text",
              name: "name",
              title: "Name of buyer:",
              isRequired: true,
              requiredErrorText: "Please Enter buyer name."
            },
            {
              type: "text",
              name: "Date",
              title: "Date",

              isRequired: true,
              inputType: "date"
            },
            {
              type: "dropdown",
              name: "Lists",
              title: "Products List",
              isRequired: true,
              startWithNewLine: false,
              choices: [
                {
                  value: "Peripherals",
                  text: "Peripherals"
                },
                {
                  value: "Motherboard",
                  text: "Motherboard"
                },
                {
                  value: "Processor/CPU",
                  text: "Processor/CPU"
                },
                {
                  value: "Graphic Card/GPU",
                  text: "Graphic Card/GPU"
                },
                {
                  value: "Memory/RAM",
                  text: "Memory/RAM"
                },
                {
                  value: "Storage",
                  text: "Storage"
                },
                {
                  value: "Monitor",
                  text: "Monitor"
                },
                {
                  value: "Power Supply",
                  text: "Power Supply"
                }
              ]
            },
            {
              type: "dropdown",
              name: "Citys",
              title: "City Names",
              isRequired: true,
              requiredErrorText: "Please Select City.",
              choices: [
                {
                  value: "item1",
                  text: "Mumbai"
                },
                {
                  value: "item2",
                  text: "Delhi"
                },
                {
                  value: "item3",
                  text: "Bangalore"
                },
                {
                  value: "item4",
                  text: "Hyderabad"
                },
                {
                  value: "item5",
                  text: "Ahmedabad"
                },
                {
                  value: "item6",
                  text: "Kolkata"
                },
                {
                  value: "item7",
                  text: "Surat"
                },
                {
                  value: "item8",
                  text: "Pune"
                },
                {
                  value: "item9",
                  text: "Patna"
                },
                {
                  value: "item10",
                  text: "Srinagar"
                }
              ]
            },
            {
              type: "text",
              name: "price",
              inputType: "number",
              title: "Price:",
              inRequired: true,
              min: 1,
              startWithNewLine: false
            },
            {
              type: "text",
              name: "quantity",
              inputType: "number",
              title: "Quantity:",
              isRequired: true,
              startWithNewLine: true,
              min: 1,
              max: 100
            },
            {
              type: "text",
              name: "Discont",
              title: "Discont",
              startWithNewLine: false,
              min: 5,
              max: 40
            },
            {
              type: "expression",
              name: "total",
              title: "Total Item Cost:",
              expression: "{panel.price} * {panel.quantity} - {panel.Discont}",
              displayStyle: "currency",
              currency: "INR"
            }
          ],
          minPanelCount: 1,
          maxPanelCount: 1
          // panelAddText: "Add another  item",
          // panelRemoveText: "Remove item"
        }
        // {
        //   type: "panel",
        //   title: "Totals",
        //   elements: [
        //     {
        //       type: "expression",
        //       name: "totalQuantity",
        //       title: "Total  Quantity:",
        //       expression: "sumInArray({items}, 'quantity')"
        //     },
        //     {
        //       type: "expression",
        //       name: "totalCost",
        //       title: "Total Cost:",
        //       expression: "sumInArray({items}, 'total')",
        //       displayStyle: "currency",
        //       currency: "INR",
        //       startWithNewLine: false
        //     },
        //     {
        //       type: "expression",
        //       name: "totalDiscont",
        //       title: "Total Discont:",
        //       expression: "sumInArray({items}, 'Discont')",
        //       displayStyle: "currency",
        //       currency: "INR",
        //       startWithNewLine: false
        //     }
        //   ]
        // }
      ]
    };

    var model = new SurveyVue.Model(json);
    return {
      survey: model,

      posts: []
    };
  },
  created() {
    this.survey.onComplete.add(res => {
      console.log(`res.data`, res.data);
    });
  },
  methods: {
    submitData() {
      console.log(`this.survey`, this.survey);
      const data = this.survey.data;
      console.log(`data`, data);
      const monthNames = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December"
      ];

      const d = new Date();
      this.posts.push({
        name: data.items[0].name,
        Date: data.items[0].Date,
        // product: data.items[0].Lists,
        // price: data.items[0].price,
        quantity: data.totalQuantity,
        total: data.totalCost,
        Discont: data.totalDiscont
      });
      this.survey.data = {};
      console.log("The current month is " + monthNames[d.getMonth()]);
    }
  }
};
</script>