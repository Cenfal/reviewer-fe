<template>
  <div class="company-box" @mouseover="openPopup" @mouseleave="closePopup">
    <!-- Content of the company box -->
    <img :src="logo" :alt="name + ' logo'" class="company-logo" />
    <h3 class="company-name">{{ name }}</h3>
    <!-- ... other company information ... -->

    <!-- Popup -->
    <div class="popup" v-if="showPopup" :style="popupStyle">
      <div class="popup-content">
        <img :src="logo" :alt="name + ' logo'" class="popup-logo" />
        <h2 class="popup-company-name">{{ name }}</h2>
        <div class="popup-company-info">
          <div class="rating">
            <span class="average-rating">{{ averageRating }}</span>/5
          </div>
          <div class="employee-number">{{ employeeNumber }} employees</div>
          <div class="industry">{{ industry }}</div>
        </div>
        <button class="see-more-button" @click="closePopup">See More</button>
      </div>
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
    };
  },
  methods: {
    openPopup(event) {
      this.showPopup = true;
      this.position = {
        x: event.clientX + 10, // Adjust the offset as needed
        y: event.clientY + 10, // Adjust the offset as needed
      };
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
  props: {
    logo: {
      type: String,
      required: true,
    },
    name: {
      type: String,
      required: true,
    },
    averageRating: {
      type: Number,
      required: true,
    },
    employeeNumber: {
      type: Number,
      required: true,
    },
    industry: {
      type: String,
      required: true,
    },
  },
};
</script>

<style scoped>
  .company-box {
    border: 6px solid #6d1c1c;
    border-radius: 4px;
    padding: 70px;
  }
  
  .company-logo {
    max-width: 100px;
    max-height: 100px;
  }
  
  .company-name {
    margin-top: 10px;
    font-size: 18px;
  }
  
  .company-info {
    margin-top: 10px;
  }
  
  .rating {
    font-size: 16px;
    font-weight: bold;
  }
  
  .average-rating {
    color: #ff9900;
  }
  
  .employee-number,
  .industry {
    margin-top: 5px;
    font-size: 14px;
    color: #666;
  }

.popup {
  position: absolute;
  top: 100%;
  left: 0;
  z-index: 999;
  background-color: #fff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  padding: 20px;
  display: none;
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

.see-more-button {
  margin-top: 20px;
  padding: 8px 16px;
  background-color: #4c51bf;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

/* Show popup when hovering over the company box */
.company-box:hover .popup {
  display: block;
}
</style>