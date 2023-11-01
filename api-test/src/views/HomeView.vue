<script setup>
import { ref } from "vue";
import axios from "axios";

const jobPosts = ref([]);
const applicationSubmitted = ref(false);
const selectedJob = ref(null);

const getJobPosts = async () => {
  const response = await axios.get(
    "https://bti.id/services/btiportalcorems/api/pt-job-posts/no-auth"
  );
  jobPosts.value = response.data;
};
getJobPosts();

const showJobDetails = (jobTitle) => {
  selectedJob.value = jobPosts.value.find(
    (jobPost) => jobPost.title === jobTitle
  );
};

const applyForJob = async () => {
  const applicationData = {
    displayName: "test",
    subject: "Marketing Planner",
    email: "ar@bti.id",
    phone: "+11111",
    message: "test",
    ptJobApplyType: "APPLICATION",
    isActive: false,
    ptJobPost: { id: 1 },
  };

  try {
    await axios.post(
      "https://bti.id/services/btiportalcorems/api/pt-job-applies/no-auth",
      applicationData
    );
    applicationSubmitted.value = true;
  } catch (error) {
    console.error(error);
  }
};
</script>

<template>
  <main>
    <div class="container">
      <!-- <div class="job-container"> -->
      <div v-for="post in jobPosts" :key="post.id" class="job-list">
        <p>{{ post.title }}</p>
        <span @click="showJobDetails(post.title)">See Job</span>
      </div>
    <!-- </div> -->

      <div class="job-details" v-if="selectedJob">
        <h1>Job Description</h1>
        <h2>{{ selectedJob.title }}</h2>
        <hr />
        <p>{{ selectedJob.description.txt }}</p>
        <br />
        <h2>Skills Required</h2>
        <hr />

        <p v-for="skill in selectedJob.ptJobSkills" :key="skill.id">
          - {{ skill.name }}
        </p>
        <button @click="applyForJob">Apply for Job</button>
      </div>
    </div>

    <div>
      <pre>{{ jobPosts }}</pre>
    </div>

    <div id="applicationResponse">
      <p v-if="applicationSubmitted">Job application submitted successfully.</p>
    </div>
  </main>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.container {
  margin: 20px;
  border-radius: 15px;
  padding: 10px;
}
/* .job-container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
} */
.job-list {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 7px;
  color: white;
  background-color: #6c5ce7;
  border-radius: 15px;
  margin-bottom: 20px;
  /* margin-right: 20px; */
  width: 100%;
  box-shadow: 10px 10px 0px 0px rgba(0, 0, 0, 0.75);
  -webkit-box-shadow: 10px 10px 0px 0px rgba(0, 0, 0, 0.75);
  -moz-box-shadow: 10px 10px 0px 0px rgba(0, 0, 0, 0.75);
}
.job-list span {
  background-color: white;
  color: black;
  padding: 5px;
  border-radius: 15px;
  cursor: pointer;
}
.job-details {
  margin-top: 30px;
  background-color: #6c5ce7;
  color: white;
  border-radius: 15px;
  padding: 15px;
  box-shadow: 10px 10px 0px 0px rgba(0, 0, 0, 0.75);
  -webkit-box-shadow: 10px 10px 0px 0px rgba(0, 0, 0, 0.75);
  -moz-box-shadow: 10px 10px 0px 0px rgba(0, 0, 0, 0.75);
}
.job-details button {
  margin-top: 10px;
  background-color: white;
  border: none;
  padding: 5px;
  width: 100%;
  border-radius: 15px;
}
</style>
