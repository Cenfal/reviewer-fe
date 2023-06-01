<template>
    <div
      class="popup"
      v-if="showPopup"
      :style="popupStyle"
    >
      <div class="popup-content">
        <img :src="company.logo" :alt="company.name + ' logo'" class="popup-logo" />
        <h2 class="popup-company-name">{{ company.name }}</h2>
        <div class="popup-company-info">
          <div class="rating">
            <span class="average-rating">{{ company.averageRating }}</span>/5
          </div>
          <div class="employee-number">{{ company.employeeNumber }} employees</div>
          <div class="industry">{{ company.industry }}</div>
        </div>
        <button class="see-more-button" @click="closePopup">See More</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        showPopup: false,
        position: {
          x: 0,
          y: 0,
        },
        company: {},
      };
    },
    methods: {
      openPopup(event) {
        this.showPopup = true;
        this.position = {
          x: event.clientX + 10, // Adjust the offset as needed
          y: event.clientY + 10, // Adjust the offset as needed
        };
  
        // Fetch the company details from the JSON file based on the company name
        const companyName = this.name; // Assuming the name prop contains the company name
        fetch('/dummycompanyinfo.json')
          .then(response => response.json())
          .then(data => {
            const companyDetails = data.find(company => company.name === companyName);
            if (companyDetails) {
              this.company = companyDetails;
            }
          })
          .catch(error => {
            console.error('Error fetching company details:', error);
          });
      },
      closePopup() {
        this.showPopup = false;
      },
    },
    computed: {
      popupStyle() {
        return {
          top: `${this.position.y}px`,
          left: `${this.position.x}px`,
        };
      },
    },
  };
  </script>
  
  <style scoped>
  .popup {
    position: absolute;
    background-color: #fff;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    padding: 20px;
    z-index: 999;
    /* Add other styles as needed */
  }
  
  .popup-content {
    /* Add other styles as needed */
  }
  
  .popup-logo {
    max-width: 150px;
    max-height: 150px;
  }
  
  .popup-company-name {
    margin-top: 10px;
    font-size: 18px;
  }
  
  .popup-company-info {
    margin-top: 10px;
  }
  
  .see-more-button {
    margin-top: 20px;
    padding: 8px 16px;
    background-color: #4c51bf;
    color: #fff;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  </style>
  