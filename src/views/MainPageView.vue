<template>
  <div class="main-page">
    <SearchBar @search="handleSearch" />
    <h1>Company List</h1>
    <div class="company-list grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4 mt-4">
      <CompanyBox
        v-for="company in displayedCompanies"
        :key="company.id"
        :logo="company.logo"
        :name="company.name"
        :average-rating="company.averageRating"
        :employee-number="company.employeeNumber"
        :industry="company.industry"
      />
    </div>
    <button
      v-if="showSeeMoreButton"
      class="mt-4 bg-blue-500 hover:bg-blue-600 text-white font-bold py-2 px-4 rounded"
      @click="loadMoreCompanies"
    >
      See More
    </button>
  </div>
</template>

<script>
import CompanyBox from '../components/CompanyBox.vue';
import companyData from '../dummy/dummycompany.json';
import SearchBar from '../components/SearchBar.vue';

export default {
  components: {
    CompanyBox,
    SearchBar,
  },
  data() {
    return {
      companies: [],
      filteredCompanies: [],
      itemsPerPage: 20,
      currentPage: 1,
    };
  },
  computed: {
    displayedCompanies() {
      const startIndex = (this.currentPage - 1) * this.itemsPerPage;
      const endIndex = startIndex + this.itemsPerPage;
      return this.filteredCompanies.slice(startIndex, endIndex);
    },
    showSeeMoreButton() {
      return this.filteredCompanies.length > this.itemsPerPage * this.currentPage;
    },
  },
  mounted() {
    this.fetchCompanyData();
  },
  methods: {
    fetchCompanyData() {
      // Simulate an asynchronous fetch request
      setTimeout(() => {
        this.companies = companyData;
        this.filteredCompanies = companyData;
      }, 1000);
    },
    handleSearch(searchText) {
      this.currentPage = 1;
      this.filteredCompanies = this.companies.filter(company =>
        company.name.toLowerCase().includes(searchText.toLowerCase())
      );
    },
    loadMoreCompanies() {
      this.currentPage++;
    },
  },
};
</script>

<style scoped>
.main-page {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  height: 170vh;
  padding: 1rem;
  box-sizing: border-box;
}

.company-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  grid-auto-rows: 250px;
  justify-items: center;
  gap: 3rem;
  width: 100%;
  max-width: 1200px;
  margin-top: 2rem;
}

@media (max-width: 640px) {
  .company-list {
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  }
}

@media (max-width: 480px) {
  .company-list {
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  }
}
</style>