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
                <q-btn
                  label="Clear"
                  type="reset"
                  color="primary"
                  flat
                  class="q-ml-sm"
                />
              </div>
            </q-form>
          </div>
        </div>

        <q-list bordered padding class="rounded-borders">
          <q-item-label header>Search results</q-item-label>

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
                  icon="add"
                  aria-label="add"
                  @click="addItem"
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
                  icon="add"
                  aria-label="add"
                  @click="addItem"
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
              title="Application Deadline"
              subtitle="January 10"
              side="left"
            >
              Massachusetts Institute of Technology<br />
              Masters of Science in Computational Science and Engineering
            </q-timeline-entry>
            <q-timeline-entry
              title="Application Deadline"
              subtitle="January 10"
              side="left"
            >
              Massachusetts Institute of Technology<br />
              Masters of Science in Computational Science and Engineering
            </q-timeline-entry>
            <q-timeline-entry
              title="Application Deadline"
              subtitle="January 10"
              side="left"
            >
              Massachusetts Institute of Technology<br />
              Masters of Science in Computational Science and Engineering
            </q-timeline-entry>
          </q-timeline>
        </div>
      </q-card>
    </div>
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
      search_result_list: null,
    };
  },
  methods: {
    SearchProgram() {
      console.log(this.school_name);
      console.log(this.program_name);
      // console.log("haha");
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
        console.log(data);
        this.data_from_firebase = data;
      })
      .catch(() => {
        console.log("fetch error occurs");
        nanananna
        sasdqwdqwdwq
      });
  },
});
</script>
