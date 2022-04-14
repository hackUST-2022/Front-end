<template>
  <q-page class="flex flex-center">
    <div class="q-pa-md">
      <q-card>
        <div class="q-pa-md">
          <div class="row">
            <q-form @submit.prevent @reset="onReset" class="q-gutter-md">
              <q-select
                style="width: 350px"
                filled
                label="School Name"
                v-model="school_name"
                use-input
                hide-selected
                fill-input
                input-debounce="0"
                :options="school_name_options"
                @filter="school_name_filter"
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
            style="max-width: 523px"
            >
            <template v-slot:header>
              <q-item-section>
                <q-item-label lines="1">{{
                  search_result_item.program_name
                }}</q-item-label>
                <q-item-label caption
                  >Degree: {{ search_result_item.degree }}</q-item-label
                >
              </q-item-section>

              <q-item-section side>
                <q-btn
                  flat
                  dense
                  round
                  icon="add"
                  aria-label="add"
                  @click="addItem"
                />
              </q-item-section>
            </template>

            <q-card>
              <q-list>
                <q-item>
                  <q-item-section>
                    <q-item-label>Application deadline</q-item-label>
                    <q-item-label caption lines="2">{{
                      search_result_item.application_deadline
                    }}</q-item-label>
                  </q-item-section>
                </q-item>
                <q-item>
                  <q-item-section>
                    <q-item-label>Requirements</q-item-label>
                    <q-item-label caption lines="2">{{
                      search_result_item.requirements
                    }}</q-item-label>
                  </q-item-section>
                </q-item>
                <q-item>
                  <q-item-section>
                    <q-item-label>Term of enrollment</q-item-label>
                    <q-item-label caption lines="2">{{
                      search_result_item.term_of_enrollment
                    }}</q-item-label>
                  </q-item-section>
                </q-item>
                <q-item>
                  <q-item-section>
                    <q-item-label color="primary" flat class="q-ml-sm">
                      <a
                        :href="search_result_item.program_website"
                        target="_blank"
                        >Visit program website</a
                      >
                    </q-item-label>
                  </q-item-section>
                </q-item>
                <q-item>
                  <q-item-section>
                    <q-item-label>Watch tutorial</q-item-label>
                    <iframe
                      width="385"
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
            expand-icon-toggle
            expand-separator
            style="max-width: 523px"
          >
            <template v-slot:header>
              <q-item-section>
                <q-item-label lines="1"
                  >Computational Science and Engineering SM</q-item-label
                >
                <q-item-label caption
                  >Degree: Masters of Science in Computational Science and
                  Engineering</q-item-label
                >
              </q-item-section>

              <q-item-section side>
                <q-btn
                  flat
                  dense
                  round
                  icon="remove"
                  aria-label="remove"
                  @click="removeItem"
                />
              </q-item-section>
            </template>

            <q-card>
              <q-list>
                <q-item>
                  Application deadline: January 10th <br /><br />
                  Requirements: Online application;Statement of objectives;Three
                  letters of recommendation;Transcripts;English proficiency exam
                  scores;GRE scores (not required for the 2021-2022 application
                  cycle);CV or Résumé<br /><br />
                  Term of enrollment: Fall Term (September)<br />
                  <a href="https://gradadmissions.mit.edu/programs/csesm"
                    >Visit program website</a
                  >
                </q-item>
              </q-list>
            </q-card>
          </q-expansion-item>
          <q-expansion-item
            expand-icon-toggle
            expand-separator
            style="max-width: 523px"
            >>
            <template v-slot:header>
              <q-item-section>
                <q-item-label lines="1"
                  >Computational Science and Engineering SM</q-item-label
                >
                <q-item-label caption
                  >Degree: Masters of Science in Computational Science and
                  Engineering</q-item-label
                >
              </q-item-section>

              <q-item-section side>
                <q-btn
                  flat
                  dense
                  round
                  icon="remove"
                  aria-label="remove"
                  @click="removeItem"
                />
              </q-item-section>
            </template>

            <q-card>
              <q-list>
                <q-item>
                  Application deadline: January 10th <br /><br />
                  Requirements: Online application;Statement of objectives;Three
                  letters of recommendation;Transcripts;English proficiency exam
                  scores;GRE scores (not required for the 2021-2022 application
                  cycle);CV or Résumé<br /><br />
                  Term of enrollment: Fall Term (September)<br />
                  <a href="https://gradadmissions.mit.edu/programs/csesm"
                    >Visit program website</a
                  >
                </q-item>
              </q-list>
            </q-card>
          </q-expansion-item>
          <q-expansion-item
            expand-icon-toggle
            expand-separator
            style="max-width: 523px"
            >>
            <template v-slot:header>
              <q-item-section>
                <q-item-label lines="1"
                  >Computational Science and Engineering SM</q-item-label
                >
                <q-item-label caption
                  >Degree: Masters of Science in Computational Science and
                  Engineering</q-item-label
                >
              </q-item-section>

              <q-item-section side>
                <q-btn
                  flat
                  dense
                  round
                  icon="remove"
                  aria-label="remove"
                  @click="removeItem"
                />
              </q-item-section>
            </template>

            <q-card>
              <q-list>
                <q-item>
                  Application deadline: January 10th <br /><br />
                  Requirements: Online application;Statement of objectives;Three
                  letters of recommendation;Transcripts;English proficiency exam
                  scores;GRE scores (not required for the 2021-2022 application
                  cycle);CV or Résumé<br /><br />
                  Term of enrollment: Fall Term (September)<br />
                  <a href="https://gradadmissions.mit.edu/programs/csesm"
                    >Visit program website</a
                  >
                </q-item>
              </q-list>
            </q-card>
          </q-expansion-item>
        </q-list>
      </q-card>

      <q-card>
        <div class="q-pa-lg">
          <q-timeline
            :layout="layout"
            :side="side"
            color="secondary"
            style="max-width: 350"
          >
            <q-timeline-entry heading>Application timeline</q-timeline-entry>

            <q-timeline-entry
              v-for="timeline_item in timeline_list"
              :key="timeline_item.program_id"
              :title="timeline_item.program_name"
              :subtitle="timeline_item.now_time"
              side="left"
            >
              Institute: {{ timeline_item.school_name }}<br />
              Degree: {{ timeline_item.degree }}<br />
            </q-timeline-entry>
          </q-timeline>
        </div>
      </q-card>
      <q-btn @click="TempJsonLoader">test</q-btn>
      <q-btn @click="ApplicationTimelineLoader">test2</q-btn>
      {{ selected_program_list }}
      {{ timeline_list }}
    </div>
    <q-dialog v-model="alert">
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
      alert: false,
    };
  },
  methods: {
    SearchProgram() {
      this.search_result_list = [];
      console.log(this.school_name);
      console.log(this.program_name);
      let SchoolName = this.school_name;
      let ProgramName = this.program_name;
      // console.log("haha");
      if (SchoolName == "") {
        console.log("error!!!!");
        this.alert = true;
        return;
      }
      while (SchoolName.indexOf(" ") != -1) {
        SchoolName = SchoolName.replace(" ", "_");
      }
      console.log(SchoolName);
      const school = this.data_from_firebase[SchoolName];
      console.log(JSON.stringify(this.data_from_firebase));
      console.log(
        JSON.stringify(this.data_from_firebase["Stanford_University"]["AE"])
      );
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
          return 10;
          break;
        case "Nov":
          return 11;
          break;
        case "Dec":
          return 12;
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
