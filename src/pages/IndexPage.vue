<template>
  <q-page class="flex flex-center">
    <div class="q-pa-md">
      <q-card>
        <div class="q-pa-md">
          <div class="row">
            <q-form @submit.prevent class="q-gutter-md">
              <q-select
                style="width: 340px"
                filled
                label="School Name"
                v-model="school_name"
                use-input
                hide-selected
                fill-input
                input-debounce="0"
                :options="school_name_options"
              >
                <template v-slot:no-option>
                  <q-item>
                    <q-item-section class="text-grey">
                      No results
                    </q-item-section>
                  </q-item>
                </template>
              </q-select>
              <q-input filled v-model="program_name" label="Program name" />
              <div>
                <q-btn
                  label="Search Program"
                  type="submit"
                  color="primary"
                  @click="SearchProgram()"
                />
              </div>
            </q-form>
          </div>
        </div>

        <q-list bordered padding class="rounded-borders">
          <q-item-label header>Search results</q-item-label>

          <q-expansion-item
            v-for="search_result_item in search_result_list"
            :key="search_result_item.program_id"
            expand-icon-toggle
            expand-separator
            style="max-width: 340px"
          >
            <template v-slot:header>
              <q-item-section>
                <q-item-label lines="1">{{
                  search_result_item.program_name
                }}</q-item-label>
                <q-item-label caption
                  >Degree:
                  <q-list>
                    <q-item
                      v-for="(degree_item, key) in search_result_item.degree"
                      :key="key"
                    >
                      <q-item-section>{{ degree_item }}</q-item-section>
                    </q-item>
                  </q-list>
                </q-item-label>
              </q-item-section>

              <q-item-section side>
                <q-btn
                  flat
                  dense
                  round
                  icon="add"
                  aria-label="add"
                  @click="addItem(search_result_item)"
                />
              </q-item-section>
            </template>

            <q-card>
              <q-list bordered separator>
                <q-item>
                  <q-item-section>
                    <q-item-label>Term of Enrollment</q-item-label>
                    <q-item-label caption lines="2">
                      <q-list bordered separator>
                        <q-item
                          v-for="(
                            term_of_enrollment_item, key
                          ) in search_result_item.term_of_enrollment"
                          :key="key"
                        >
                          <q-item-section>{{
                            term_of_enrollment_item
                          }}</q-item-section>
                        </q-item>
                      </q-list>
                    </q-item-label>
                  </q-item-section>
                </q-item>
                <q-item>
                  <q-item-section>
                    <q-item-label>Application deadline</q-item-label>
                    <q-item-label caption lines="2">
                      <!-- {{
                      search_result_item.application_deadline
                    }} -->

                      <q-list bordered separator>
                        <q-item
                          v-for="(
                            date_item, key
                          ) in search_result_item.application_deadline"
                          :key="key"
                        >
                          <q-item-section>{{ date_item }}</q-item-section>
                        </q-item>
                      </q-list>
                    </q-item-label>
                  </q-item-section>
                </q-item>
                <q-item>
                  <q-item-section>
                    <q-item-label>Requirements</q-item-label>
                    <q-item-label caption lines="2">
                      <q-list bordered separator>
                        <q-item
                          v-for="(
                            requirement_item, key
                          ) in search_result_item.requirements"
                          :key="key"
                        >
                          <q-item-section>{{
                            requirement_item
                          }}</q-item-section>
                        </q-item>
                      </q-list>
                    </q-item-label>
                  </q-item-section>
                </q-item>
                <q-item>
                  <q-item-section>
                    <q-item-label>Research Area</q-item-label>
                    <q-item-label caption lines="2">
                      <q-list bordered separator>
                        <q-item
                          v-for="(
                            research_area_item, key
                          ) in search_result_item.research_area"
                          :key="key"
                        >
                          <q-item-section>{{
                            research_area_item
                          }}</q-item-section>
                        </q-item>
                      </q-list>
                    </q-item-label>
                  </q-item-section>
                </q-item>
                <q-item>
                  <q-item-section>
                    <q-item-label>Interdisciplinary Programs</q-item-label>
                    <q-item-label caption lines="2">
                      <q-list bordered separator>
                        <q-item
                          v-for="(
                            interdisciplinary_program_item, key
                          ) in search_result_item.interdisciplinary_program"
                          :key="key"
                        >
                          <q-item-section>{{
                            interdisciplinary_program_item
                          }}</q-item-section>
                        </q-item>
                      </q-list>
                    </q-item-label>
                  </q-item-section>
                </q-item>
                <q-item>
                  <q-item-section>
                    <q-item-label color="primary" flat class="q-ml-sm">
                      <q-btn
                        :href="search_result_item.program_website"
                        target="_blank"
                        >Visit program website</q-btn
                      >
                      <q-btn>Contact Advisor</q-btn>
                    </q-item-label>
                  </q-item-section>
                </q-item>
                <q-item>
                  <q-item-section>
                    <q-item-label>Watch tutorial</q-item-label>
                    <iframe
                      width="340"
                      height="216"
                      src="https://www.youtube.com/embed/huYmEFkd5Y8"
                      title="YouTube video player"
                      frameborder="0"
                      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                      allowfullscreen
                    ></iframe>
                  </q-item-section>
                </q-item>
              </q-list>
            </q-card>
          </q-expansion-item>
        </q-list>
      </q-card>
      <q-card class="q-mt-md">
        <q-list bordered padding class="rounded-borders">
          <q-item-label header>Selected programs</q-item-label>

          <q-expansion-item
            v-for="selected_program_item in selected_program_list"
            :key="selected_program_item.program_id"
            expand-icon-toggle
            expand-separator
            style="max-width: 340px"
          >
            <template v-slot:header>
              <q-item-section>
                <q-item-label lines="1">
                  {{ selected_program_item.program_name }}
                </q-item-label>
                <q-item-label caption
                  >Degree:
                  <q-list>
                    <q-item
                      v-for="(degree_item, key) in selected_program_item.degree"
                      :key="key"
                    >
                      <q-item-section>{{ degree_item }}</q-item-section>
                    </q-item>
                  </q-list>
                </q-item-label>
              </q-item-section>
              <q-item-section side>
                <q-btn
                  flat
                  dense
                  round
                  icon="remove"
                  aria-label="remove"
                  @click="removeItem(selected_program_item)"
                />
              </q-item-section>
            </template>

            <q-card>
              <q-list bordered separator>
                <q-item>
                  <q-item-section>
                    <q-item-label>Term of Enrollment</q-item-label>
                    <q-item-label caption lines="2">
                      <q-list bordered separator>
                        <q-item
                          v-for="(
                            term_of_enrollment_item, key
                          ) in selected_program_item.term_of_enrollment"
                          :key="key"
                        >
                          <q-item-section>{{
                            term_of_enrollment_item
                          }}</q-item-section>
                        </q-item>
                      </q-list>
                    </q-item-label>
                  </q-item-section>
                </q-item>
                <q-item>
                  <q-item-section>
                    <q-item-label>Application deadline</q-item-label>
                    <q-item-label caption lines="2">
                      <!-- {{
                      selected_program_item.application_deadline
                    }} -->
                      <q-list bordered separator>
                        <q-item
                          v-for="(
                            date_item, key
                          ) in selected_program_item.application_deadline"
                          :key="key"
                        >
                          <q-item-section>{{ date_item }}</q-item-section>
                        </q-item>
                      </q-list>
                    </q-item-label>
                  </q-item-section>
                </q-item>
                <q-item>
                  <q-item-section>
                    <q-item-label>Requirements</q-item-label>
                    <q-item-label caption lines="2">
                      <q-list bordered separator>
                        <q-item
                          v-for="(
                            requirement_item, key
                          ) in selected_program_item.requirements"
                          :key="key"
                        >
                          <q-item-section>{{
                            requirement_item
                          }}</q-item-section>
                        </q-item>
                      </q-list>
                    </q-item-label>
                  </q-item-section>
                </q-item>
                <q-item>
                  <q-item-section>
                    <q-item-label>Research Area</q-item-label>
                    <q-item-label caption lines="2">
                      <q-list bordered separator>
                        <q-item
                          v-for="(
                            research_area_item, key
                          ) in selected_program_item.research_area"
                          :key="key"
                        >
                          <q-item-section>{{
                            research_area_item
                          }}</q-item-section>
                        </q-item>
                      </q-list>
                    </q-item-label>
                  </q-item-section>
                </q-item>
                <q-item>
                  <q-item-section>
                    <q-item-label>Interdisciplinary Programs</q-item-label>
                    <q-item-label caption lines="2">
                      <q-list bordered separator>
                        <q-item
                          v-for="(
                            interdisciplinary_program_item, key
                          ) in selected_program_item.interdisciplinary_program"
                          :key="key"
                        >
                          <q-item-section>{{
                            interdisciplinary_program_item
                          }}</q-item-section>
                        </q-item>
                      </q-list>
                    </q-item-label>
                  </q-item-section>
                </q-item>
                <q-item>
                  <q-item-section>
                    <q-item-label color="primary" flat class="q-ml-sm">
                      <q-btn
                        :href="selected_program_item.program_website"
                        target="_blank"
                        >Visit program website</q-btn
                      >
                      <q-btn>Contact Advisor</q-btn>
                    </q-item-label>
                  </q-item-section>
                </q-item>
                <q-item>
                  <q-item-section>
                    <q-item-label>Watch tutorial</q-item-label>
                    <iframe
                      width="340"
                      height="216"
                      src="https://www.youtube.com/embed/huYmEFkd5Y8"
                      title="YouTube video player"
                      frameborder="0"
                      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                      allowfullscreen
                    ></iframe>
                  </q-item-section>
                </q-item>
              </q-list>
            </q-card>
          </q-expansion-item>
        </q-list>
      </q-card>
      <q-card>
        <div class="q-pa-lg">
          <text style="font-size: 32px">Application requirements</text>
          <q-list bordered separator style="max-width: 340px">
            <q-item
              v-for="(requirements_item, key) in requirement_list"
              :key="key"
            >
              <q-item-section>{{ requirements_item }}</q-item-section>
            </q-item>
          </q-list>
        </div>
      </q-card>
      <q-card>
        <div class="q-pa-lg">
          <q-timeline
            :layout="layout"
            :side="side"
            color="secondary"
            style="max-width: 350"
          >
            <text style="font-size: 32px">Application timeline</text>

            <q-timeline-entry
              v-for="timeline_item in timeline_list"
              :key="timeline_item.program_id"
              :title="timeline_item.program_name"
              :subtitle="timeline_item.now_time"
              side="left"
            >
              Institute: {{ timeline_item.school_name }}<br />
            </q-timeline-entry>
          </q-timeline>
        </div>
      </q-card>
    </div>
    <q-dialog v-model="search_alert">
      <q-card>
        <q-card-section>
          <div class="text-h6">Alert</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          Please select a school name.
        </q-card-section>

        <q-card-actions align="right">
          <q-btn flat label="OK" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>

    <q-dialog v-model="add_alert">
      <q-card>
        <q-card-section>
          <div class="text-h6">Alert</div>
        </q-card-section>

        <q-card-section class="q-pt-none">
          The program was already added.
        </q-card-section>

        <q-card-actions align="right">
          <q-btn flat label="OK" color="primary" v-close-popup />
        </q-card-actions>
      </q-card>
    </q-dialog>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "IndexPage",
  data() {
    return {
      school_name_options: [
        "Massachusetts Institute of Technology",
        "Stanford University",
      ],
      school_name: "",
      program_name: "",
      data_from_firebase: null,
      search_result_list: [],
      selected_program_list: [],
      timeline_list: [],
      requirement_list: new Set(),
      search_alert: false,
      add_alert: false,
    };
  },
  methods: {
    addItem(item) {
      for (let currProgram in this.selected_program_list) {
        if (
          item["program_id"] ==
          this.selected_program_list[currProgram]["program_id"]
        ) {
          // window alert
          this.add_alert = true;
          // return
          return;
        }
      }
      this.selected_program_list.push(item); //? now know the id, how to push original item inside
      this.ApplicationTimelineLoader();
      this.RequirementListLoader();
    },
    RequirementListLoader() {
      this.requirement_list = new Set();
      for (let i = 0; i < this.selected_program_list.length; i++) {
        const element = this.selected_program_list[i];
        for (let j = 0; j < element["requirements"].length; j++) {
          this.requirement_list.add(element["requirements"][j]);
        }
      }
      console.log("requirement_list");
      console.log("requirement_list");
      console.log("requirement_list");
      console.log("requirement_list");
      console.log("requirement_list");
      console.log("requirement_list");
      console.log("requirement_list");
      console.log(requirement_list);
    },
    removeItem(item) {
      // this.selected_program_list.splice(item);
      this.selected_program_list = this.selected_program_list.filter(function (
        value,
        index,
        arr
      ) {
        return value != item;
      });
      //update time line
      this.ApplicationTimelineLoader();
      this.RequirementListLoader();
    },
    SearchProgram() {
      this.search_result_list = [];
      console.log(this.school_name);
      console.log(this.program_name);
      let SchoolName = this.school_name;
      let ProgramName = this.program_name;
      // console.log("haha");
      if (SchoolName == "") {
        console.log("error!!!!");
        this.search_alert = true;
        return;
      }
      while (SchoolName.indexOf(" ") != -1) {
        SchoolName = SchoolName.replace(" ", "_");
      }
      console.log(SchoolName);
      const school = this.data_from_firebase[SchoolName];
      console.log(JSON.stringify(this.data_from_firebase));

      console.log("JSON.stringify(school):");
      console.log(JSON.stringify(school));
      for (var currProgram in school) {
        console.log(JSON.stringify(school[currProgram]));
        console.log("currProgram[this.program_name]");
        console.log(school[currProgram]["program_name"]);
        if (
          school[currProgram]["program_name"]
            .toLowerCase()
            .indexOf(ProgramName.toLowerCase()) != -1
        ) {
          console.log("haha");
          this.search_result_list.push(school[currProgram]);
        }
      }
      console.log(JSON.stringify(this.search_result_list));
    },
    TempJsonLoader() {
      const DataFromFirebase = this.data_from_firebase;
      this.selected_program_list = [];
      for (const i in DataFromFirebase) {
        if (Object.hasOwnProperty.call(DataFromFirebase, i)) {
          const school = DataFromFirebase[i];
          for (const j in school) {
            if (Object.hasOwnProperty.call(school, j)) {
              const program = school[j];
              this.selected_program_list.push(program);
            }
          }
        }
      }

      console.log(JSON.stringify(this.selected_program_list));
    },
    MonthStringToInt(MonthStringFirst3) {
      switch (MonthStringFirst3) {
        case "Jan":
          return 1;
          break;
        case "Feb":
          return 2;
          break;
        case "Mar":
          return 3;
          break;
        case "Apr":
          return 4;
          break;
        case "May":
          return 5;
          break;
        case "Jun":
          return 6;
          break;
        case "Jul":
          return 7;
          break;
        case "Aug":
          return 8;
          break;
        case "Sep":
          return 9;
          break;
        case "Oct":
          return -2;
          break;
        case "Nov":
          return -1;
          break;
        case "Dec":
          return 0;
          break;
        default:
          alert("date error");
      }
    },
    ApplicationTimelineLoader() {
      this.timeline_list = [];
      const SelectedPrograms = this.selected_program_list;
      for (let i = 0; i < SelectedPrograms.length; i++) {
        const program = SelectedPrograms[i];
        for (let i = 0; i < program["application_deadline"].length; i++) {
          const time = program["application_deadline"][i];
          let this_time_program = JSON.parse(JSON.stringify(program));
          while (this_time_program["school_name"].indexOf("_") != -1) {
            this_time_program["school_name"] = this_time_program[
              "school_name"
            ].replace("_", " ");
          }
          this_time_program["now_time"] = time;
          console.log(time);
          this.timeline_list.push(this_time_program);
        }
      }
      console.log(JSON.stringify(this.timeline_list));
      this.timeline_list = this.timeline_list.sort((a, b) => {
        const a_month = this.MonthStringToInt(a["now_time"].slice(0, 3));
        const b_month = this.MonthStringToInt(b["now_time"].slice(0, 3));
        const a_date = a["now_time"].slice(-2);
        const b_date = b["now_time"].slice(-2);

        if (a_month > b_month) {
          return 1;
        } else if (a_month < b_month) {
          return -1;
        } else if (a_month == b_month) {
          if (a_date > b_date) {
            return 1;
          } else if (a_date == b_date) {
            return 0;
          } else if (a_date < b_date) {
            return -1;
          }
        }
      });
    },
  },
  mounted() {
    const url =
      "https://hackust-school-info-default-rtdb.asia-southeast1.firebasedatabase.app/school_info.json";
    fetch(url)
      .then((response) => {
        return response.json();
      })
      .then((data) => {
        console.log(JSON.stringify(data));
        this.data_from_firebase = data;
      })
      .catch(() => {
        console.log("fetch error occurs");
      });
  },
});
</script>
