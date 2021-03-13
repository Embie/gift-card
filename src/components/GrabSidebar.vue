<template>
  <div class="brand-wrapper">
    <!--Brand logo and name section-->
    <div class="section">
      <!--Brand logo -->
      <div class="columns brand-logo">
        <div class="column is-12">
          <img :src="require('@/assets/grab.png')" />
        </div>
      </div>
      <hr class="divider" />
      <!--Brand Name -->
      <div class="columns brand-name">
        <div class="column is-12">
          <h1>grab</h1>
        </div>
      </div>
      <div class="columns">
        <div class="column is-4"></div>
        <div class="column is-4">
          <div class="state">active</div>
        </div>
      </div>
    </div>
    <hr class="divider" />
    <!--Feature details -->
    <div class="columns brand-feature-details">
      <div class="column is-6">
        <div class="feature-details-label">Country</div>
        <div class="featured-details-data">
          {{ brandData.featuredDetails.country }}
        </div>
      </div>
      <span class="vertical-line"></span>
      <div class="column is-3">
        <div class="feature-details-label">Products</div>
        <div class="featured-details-data">
          {{ brandData.featuredDetails.products }}
        </div>
      </div>
    </div>
    <hr class="divider" />
    <!--Details etails -->
    <div class="section">
      <div class="columns brand-details">
        <div class="column is-6">
          <div class="details-label">Id</div>
          <div class="details-data">{{ brandData.details.id }}</div>
        </div>
      </div>
      <div class="columns brand-details">
        <div class="column is-6">
          <div class="details-label">Company</div>
          <div class="details-data">{{ brandData.details.company }}</div>
        </div>
      </div>
      <div class="columns brand-details">
        <div class="column is-6">
          <div class="details-label">Category</div>
          <div class="details-data">{{ brandData.details.category }}</div>
        </div>
      </div>
      <div class="columns brand-details">
        <div class="column is-7">
          <div class="details-label">Phone</div>
          <div class="details-data margin-bottom-10">
            {{ brandData.details.phone }}
          </div>
        </div>
      </div>
    </div>
    <hr class="divider" />
    <!--Keywords  -->
    <div class="keywords">
      <div class="columns">
        <div class="column is-5">
          <div class="keywords-label">Keywords</div>
        </div>
      </div>
      <div class="columns brand-keywords">
        <div
          class="column is-4 keyword-column"
          v-for="keyword in brandData.keywords.slice(0, 5)"
          :key="keyword"
        >
          <div class="keyword">{{ keyword }}</div>
        </div>
      </div>
      <div class="columns brand-keywords">
        <div
          class="column is-4 keyword-column"
          v-for="keyword in brandData.keywords.slice(4, 5)"
          :key="keyword"
        >
          <div class="keyword">{{ keyword }}</div>
        </div>
        <div class="column is-2">
          <b-button type="is-light" class="keyword-icon">+5</b-button>
        </div>
      </div>
    </div>
    <hr class="divider" />
    <!--Icons -->
    <div class="icons-section margin-bottom-10">
      <div class="columns">
        <div class="column is-3">
          <a href="//www.google.com/">
            <b-icon icon="microsoft" size="is-small" type="is-success is-light">
            </b-icon>
          </a>
        </div>
        <div class="column is-3">
          <a href="//www.google.com/">
            <b-icon icon="facebook" size="is-small" type="is-success is-light">
            </b-icon>
          </a>
        </div>
        <div class="column is-3">
          <a href="//www.google.com/">
            <b-icon icon="instagram" size="is-small" type="is-success is-light">
            </b-icon>
          </a>
        </div>
        <div class="column is-3">
          <a href="//www.google.com/">
            <b-icon icon="twitter" size="is-small" type="is-success is-light">
            </b-icon>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
debugger
export default {
  name: 'Grab',
  data () {
    return {
      brandData: null
    }
  },
  created () {
    fetch('https://api.mocki.io/v1/5c1d3f35')
      .then(response => response.json())
      .then(data => (this.brandData = data))
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.brand-wrapper {
  border: 1px solid #fbfbfc !important;
  background-color: white;
}

.brand-logo img {
  padding: 40px;
}

.brand-name {
  font-size: 22px;
  color: #1e2226;
  font-weight: 600;
  text-transform: uppercase;
  font-weight: bold;
  margin-bottom: 0px;
}

.state {
  font-size: 12px;
  color: #1ebc7c;
  font-weight: 400;
  height: 20px;
  border-radius: 5px;
  background-color: rgba(30, 188, 124, 0.10196078431372549);
  max-height: 100%;
  margin-bottom: 11px;
}

.details-label,
.keywords-label {
  font-size: 12px;
  color: #787c80;
  font-weight: 500;
  text-align: left !important;
}

.brand-details {
  padding-left: 10px;
}

.feature-details-label {
  font-size: 12px;
  color: #787c80;
  font-weight: 500;
}

.details-data {
  font-size: 14px;
  color: #3c4044;
  font-weight: 400;
  text-align: left !important;
}

.keyword-column {
  padding-left: 18px;
  padding-right: 20px;
}
.keywords-label {
  padding-left: 10px;
}

.keyword {
  height: 20px;
  border-radius: 5px;
  background-color: #f0f2f4;
  font-size: 12px;
  color: #3c4044;
  font-weight: 400;
  font-family: "Poppins";
}

.keyword-icon {
  font-size: 12px;
  color: #1ebc7c;
  font-weight: 500;
  font-size: 11px;
  color: #007cf8;
  font-family: "Font Awesome5 Pro";
  width: 45px;
  height: 20px;
  border-radius: 5px;
  margin-bottom: 21px;
  background-color: rgba(0, 124, 248, 0.10196078431372549);
}

.vertical-line {
  width: 1px;
  height: 60px;
  background-color: #f0f2f4;
}

.divider {
  width: 315px;
  height: 1px;
  background-color: #f0f2f4;
  margin-top: -18px;
  margin-bottom: 13px;
}

.margin-bottom-10 {
  margin-bottom: 5px;
}
</style>
