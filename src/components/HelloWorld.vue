<template>
  <div class="page-container">
    <!-- Landing Page -->
    <div v-if="!isLoggedIn">
      <!-- Header -->
      <header class="header">
        <div class="header-content">
          <div class="header-brand">
            <ShieldIcon class="shield-icon" />
            <div>
              <h1 class="brand-title">BARANGAY TALAMBAN</h1>
              <p class="brand-subtitle">Official Website</p>
            </div>
          </div>
          <div class="auth-buttons">
            <button @click="showRegisterModal = true" class="register-btn">REGISTER</button>
            <button @click="showLoginModal = true" class="login-btn">LOGIN</button>
          </div>
        </div>
      </header>

      <!-- Hero Section -->
      <section class="hero-section">
        <div class="hero-content">
          <h2 class="hero-title">
            Welcome to<br />
            <span class="hero-highlight">Barangay Talamban</span>
          </h2>
          <p class="hero-description">
            Discover our community services, connect with local government, and stay informed about our barangay initiatives.
          </p>
          <div class="search-container">
            <input 
              type="text"
              placeholder="Search services, announcements, or information..."
              class="search-input"
            />
            <button class="search-btn">SEARCH</button>
          </div>
        </div>
      </section>

      <!-- Features Section -->
      <section class="features-section">
        <div class="features-content">
          <div class="section-header">
            <h3 class="section-title">
              Our <span class="title-highlight">Features</span>
            </h3>
          </div>
          <div class="features-grid">
            <div 
              v-for="(feature, index) in features"
              :key="index"
              class="feature-card"
            >
              <component :is="feature.icon" class="feature-icon" />
              <h4 class="feature-title">{{ feature.title }}</h4>
              <p class="feature-description">{{ feature.description }}</p>
            </div>
          </div>
        </div>
      </section>

      <!-- Mission & Vision Section -->
      <section class="mission-section">
        <div class="mission-content">
          <div class="section-header">
            <h3 class="mission-title">
              Mission & <span class="title-highlight-yellow">Vision</span>
            </h3>
          </div>
          <div class="mission-grid">
            <div class="mission-image-container">
              <img 
                src="./placeholder.svg?height=300&width=500"
                alt="Barangay Building"
                class="mission-image"
              />
            </div>
            <div class="mission-text">
              <div class="mission-item">
                <h4 class="mission-subtitle">Our Mission</h4>
                <p class="mission-description">
                  To provide efficient, transparent, and responsive governance that promotes the welfare and development of our community while preserving our cultural heritage and environmental sustainability.
                </p>
              </div>
              <div class="mission-item">
                <h4 class="mission-subtitle">Our Vision</h4>
                <p class="mission-description">
                  A progressive, peaceful, and prosperous Barangay Talamban where every resident enjoys quality life, equal opportunities, and active participation in community development.
                </p>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- Team Section -->
      <section class="team-section">
        <div class="team-content">
          <div class="section-header">
            <h3 class="section-title">
              The <span class="title-highlight">Barangay Officials</span>
            </h3>
          </div>
          <div class="team-grid">
            <div 
              v-for="(member, index) in teamMembers"
              :key="index"
              class="team-card"
            >
              <img 
                :src="member.image"
                :alt="member.name"
                class="team-image"
              />
              <h4 class="team-name">{{ member.name }}</h4>
              <p class="team-position">{{ member.position }}</p>
              <p class="team-description">{{ member.description }}</p>
            </div>
          </div>
        </div>
      </section>

      <!-- Footer CTA Section -->
      <section class="footer-section">
        <div class="footer-content">
          <h3 class="footer-title">
            Report, Manage, Resolve,<br />
            All in One Place.
          </h3>
          <button class="cta-btn">GET STARTED</button>
        </div>
      </section>
    </div>

    <!-- Dashboard -->
    <div v-if="isLoggedIn" class="dashboard-container">
      <!-- Dashboard Header -->
      <header class="dashboard-header">
        <div class="dashboard-header-content">
          <div class="dashboard-brand">
            <ShieldIcon class="dashboard-shield-icon" />
            <div>
              <h1 class="dashboard-brand-title">BARANGAY TALAMBAN</h1>
              <p class="dashboard-brand-subtitle">Case Management System</p>
            </div>
          </div>
          <div class="dashboard-header-right">
            <p class="dashboard-time">Philippine Standard Time: {{ currentDateTime }}</p>
            <input type="search" placeholder="Search..." class="dashboard-search" />
          </div>
        </div>
        <nav class="dashboard-nav">
          <button 
            v-for="(item, index) in navItems" 
            :key="index"
            :class="['nav-item', { active: activeNav === item.name }]"
            @click="activeNav = item.name"
          >
            <component :is="item.icon" class="nav-icon" />
            {{ item.name }}
          </button>
          <button @click="logout" class="logout-btn">
            <LogOut class="nav-icon" />
            Logout
          </button>
        </nav>
      </header>

      <!-- Dashboard Content -->
      <main class="dashboard-main">
        <div class="dashboard-content">
          <div class="dashboard-title-section">
            <h2 class="dashboard-title">USER Dashboard</h2>
            <p class="dashboard-subtitle">Manage and track your barangay cases and complaints</p>
          </div>

          <div class="dashboard-controls">
            <div class="search-filter-container">
              <div class="search-box">
                <Search class="search-icon" />
                <input 
                  type="text" 
                  placeholder="Search cases..." 
                  v-model="searchQuery"
                  class="search-input-dashboard"
                />
              </div>
              <select v-model="statusFilter" class="status-filter">
                <option value="">All Status</option>
                <option value="RESOLVED">Resolved</option>
                <option value="PENDING">Pending</option>
                <option value="IN PROGRESS">In Progress</option>
              </select>
            </div>
          </div>

          <div class="cases-container">
            <div 
              v-for="case_item in filteredCases" 
              :key="case_item.id"
              class="case-card"
            >
              <div class="case-info">
                <div class="case-header">
                  <div>
                    <p class="case-label">Case ID</p>
                    <p class="case-id">{{ case_item.id }}</p>
                  </div>
                  <div>
                    <p class="case-label">Complaint Type</p>
                    <p class="case-value">{{ case_item.type }}</p>
                  </div>
                  <div>
                    <p class="case-label">Respondent</p>
                    <p class="case-value">{{ case_item.respondent }}</p>
                  </div>
                  <div>
                    <p class="case-label">Date</p>
                    <p class="case-value">{{ case_item.date }}</p>
                  </div>
                </div>
              </div>
              <div class="case-actions">
                <span :class="['status-badge', case_item.status.toLowerCase().replace(' ', '-')]">
                  {{ case_item.status }}
                </span>
                <button class="view-more-btn">
                  <Eye class="view-icon" />
                  View more
                </button>
              </div>
            </div>
          </div>

          <div class="pagination">
            <p class="pagination-info">Showing {{ startIndex }} to {{ endIndex }} of {{ totalCases }} results</p>
            <div class="pagination-controls">
              <button :disabled="currentPage === 1" @click="currentPage--" class="pagination-btn">Previous</button>
              <button 
                v-for="page in totalPages" 
                :key="page"
                :class="['pagination-btn', { active: currentPage === page }]"
                @click="currentPage = page"
              >
                {{ page }}
              </button>
              <button :disabled="currentPage === totalPages" @click="currentPage++" class="pagination-btn">Next</button>
            </div>
          </div>
        </div>
      </main>
    </div>

    <!-- Login Modal -->
    <div v-if="showLoginModal" class="modal-overlay" @click="showLoginModal = false">
      <div class="modal-content" @click.stop>
        <h3 class="modal-title">Login to Your Account</h3>
        <form @submit.prevent="handleLogin">
          <div class="form-group">
            <label>Email or Username</label>
            <input v-model="loginForm.email" type="text" required class="form-input" />
          </div>
          <div class="form-group">
            <label>Password</label>
            <input v-model="loginForm.password" type="password" required class="form-input" />
          </div>
          <div class="modal-actions">
            <button type="button" @click="showLoginModal = false" class="cancel-btn">Cancel</button>
            <button type="submit" class="submit-btn">Login</button>
          </div>
        </form>
      </div>
    </div>

    <!-- Register Modal -->
    <div v-if="showRegisterModal" class="modal-overlay" @click="showRegisterModal = false">
      <div class="modal-content" @click.stop>
        <h3 class="modal-title">Create New Account</h3>
        <form @submit.prevent="handleRegister">
          <div class="form-group">
            <label>Full Name</label>
            <input v-model="registerForm.fullName" type="text" required class="form-input" />
          </div>
          <div class="form-group">
            <label>Email</label>
            <input v-model="registerForm.email" type="email" required class="form-input" />
          </div>
          <div class="form-group">
            <label>Password</label>
            <input v-model="registerForm.password" type="password" required class="form-input" />
          </div>
          <div class="form-group">
            <label>Confirm Password</label>
            <input v-model="registerForm.confirmPassword" type="password" required class="form-input" />
          </div>
          <div class="modal-actions">
            <button type="button" @click="showRegisterModal = false" class="cancel-btn">Cancel</button>
            <button type="submit" class="submit-btn">Register</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import { 
  Shield as ShieldIcon, 
  FileText, 
  Megaphone, 
  Users, 
  Phone,
  LayoutDashboard,
  FileX,
  Calendar,
  User,
  LogOut,
  Search,
  Eye
} from 'lucide-vue-next'

// Reactive data
const isLoggedIn = ref(false)
const showLoginModal = ref(false)
const showRegisterModal = ref(false)
const currentDateTime = ref('')
const activeNav = ref('Dashboard')
const searchQuery = ref('')
const statusFilter = ref('')
const currentPage = ref(1)
const itemsPerPage = 6

// Forms
const loginForm = ref({
  email: '',
  password: ''
})

const registerForm = ref({
  fullName: '',
  email: '',
  password: '',
  confirmPassword: ''
})

// Navigation items
const navItems = [
  { name: 'Dashboard', icon: LayoutDashboard },
  { name: 'File a Complaint', icon: FileX },
  { name: 'Calendar', icon: Calendar },
  { name: 'Profile', icon: User }
]

// Sample cases data
const cases = ref([
  { id: 'Case #0001', type: 'Theft and Robbery', respondent: 'Blasminda Mayol', date: '06/19/2025', status: 'RESOLVED' },
  { id: 'Case #0002', type: 'Theft and Robbery', respondent: 'Blasminda Mayol', date: '06/19/2025', status: 'RESOLVED' },
  { id: 'Case #0003', type: 'Theft and Robbery', respondent: 'Blasminda Mayol', date: '06/19/2025', status: 'RESOLVED' },
  { id: 'Case #0004', type: 'Theft and Robbery', respondent: 'Blasminda Mayol', date: '06/19/2025', status: 'RESOLVED' },
  { id: 'Case #0005', type: 'Noise Complaint', respondent: 'Juan Dela Cruz', date: '06/20/2025', status: 'PENDING' },
  { id: 'Case #0006', type: 'Property Dispute', respondent: 'Maria Santos', date: '06/21/2025', status: 'IN PROGRESS' },
  { id: 'Case #0007', type: 'Public Disturbance', respondent: 'Pedro Garcia', date: '06/22/2025', status: 'PENDING' },
  { id: 'Case #0008', type: 'Vandalism', respondent: 'Ana Lopez', date: '06/23/2025', status: 'RESOLVED' },
  { id: 'Case #0009', type: 'Illegal Parking', respondent: 'Carlos Reyes', date: '06/24/2025', status: 'IN PROGRESS' },
  { id: 'Case #0010', type: 'Noise Complaint', respondent: 'Lisa Torres', date: '06/25/2025', status: 'PENDING' },
  { id: 'Case #0011', type: 'Theft and Robbery', respondent: 'Miguel Santos', date: '06/26/2025', status: 'RESOLVED' },
  { id: 'Case #0012', type: 'Property Dispute', respondent: 'Rosa Martinez', date: '06/27/2025', status: 'IN PROGRESS' }
])

// Features data
const features = [
  {
    icon: FileText,
    title: 'Document Services',
    description: 'Apply for barangay certificates, clearances, and permits online with ease.',
  },
  {
    icon: Megaphone,
    title: 'Announcements',
    description: 'Stay updated with the latest news, events, and important announcements.',
  },
  {
    icon: Users,
    title: 'Community Programs',
    description: 'Participate in various community programs and development initiatives.',
  },
  {
    icon: Phone,
    title: 'Emergency Services',
    description: 'Quick access to emergency contacts and reporting systems for urgent matters.',
  },
]

// Team members data
const teamMembers = [
  {
    name: 'Hon. Maria Santos',
    position: 'Barangay Captain',
    description: 'Leading our community with dedication and vision for progress.',
    image: './placeholder.svg?height=120&width=120',
  },
  {
    name: 'Juan Dela Cruz',
    position: 'Barangay Secretary',
    description: 'Managing administrative affairs and community documentation.',
    image: './placeholder.svg?height=120&width=120',
  },
  {
    name: 'Ana Rodriguez',
    position: 'Barangay Treasurer',
    description: 'Ensuring transparent financial management and accountability.',
    image: './placeholder.svg?height=120&width=120',
  },
]

// Computed properties
const filteredCases = computed(() => {
  let filtered = cases.value

  if (searchQuery.value) {
    filtered = filtered.filter(case_item => 
      case_item.id.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
      case_item.type.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
      case_item.respondent.toLowerCase().includes(searchQuery.value.toLowerCase())
    )
  }

  if (statusFilter.value) {
    filtered = filtered.filter(case_item => case_item.status === statusFilter.value)
  }

  const start = (currentPage.value - 1) * itemsPerPage
  const end = start + itemsPerPage
  return filtered.slice(start, end)
})

const totalCases = computed(() => cases.value.length)
const totalPages = computed(() => Math.ceil(totalCases.value / itemsPerPage))
const startIndex = computed(() => (currentPage.value - 1) * itemsPerPage + 1)
const endIndex = computed(() => Math.min(currentPage.value * itemsPerPage, totalCases.value))

// Methods
const updateDateTime = () => {
  const now = new Date()
  const options = {
    weekday: 'long',
    year: 'numeric',
    month: 'long',
    day: 'numeric',
    hour: '2-digit',
    minute: '2-digit',
    second: '2-digit',
    timeZone: 'Asia/Manila'
  }
  currentDateTime.value = now.toLocaleDateString('en-US', options) + ' PHT'
}

const handleLogin = () => {
  // Simple validation - in real app, you'd validate against a backend
  if (loginForm.value.email && loginForm.value.password) {
    isLoggedIn.value = true
    showLoginModal.value = false
    // Reset form
    loginForm.value = { email: '', password: '' }
  }
}

const handleRegister = () => {
  // Simple validation
  if (registerForm.value.password !== registerForm.value.confirmPassword) {
    alert('Passwords do not match!')
    return
  }
  
  if (registerForm.value.fullName && registerForm.value.email && registerForm.value.password) {
    // In a real app, you'd send this to a backend
    alert('Registration successful! Please login.')
    showRegisterModal.value = false
    showLoginModal.value = true
    // Reset form
    registerForm.value = { fullName: '', email: '', password: '', confirmPassword: '' }
  }
}

const logout = () => {
  isLoggedIn.value = false
  activeNav.value = 'Dashboard'
  currentPage.value = 1
  searchQuery.value = ''
  statusFilter.value = ''
}

// Lifecycle
onMounted(() => {
  updateDateTime()
  setInterval(updateDateTime, 1000)
})
</script>

<style scoped>
/* Base Styles */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html, body {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
}

.page-container {
  height: 100vh;
  width: 100%;
  margin: 0;
  padding: 0;
  background-color: white;
}

/* Header Styles */
.header {
  background-color: #1d4ed8;
  color: white;
  padding: 1rem 0;
}

.header-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.header-brand {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.shield-icon {
  height: 2.5rem;
  width: 2.5rem;
  color: #fbbf24;
}

.brand-title {
  font-size: 1.25rem;
  font-weight: bold;
  margin: 0;
}

.brand-subtitle {
  font-size: 0.875rem;
  opacity: 0.9;
  margin: 0;
}

.auth-buttons {
  display: flex;
  gap: 0.5rem;
}

.register-btn {
  background-color: transparent;
  color: white;
  font-weight: bold;
  padding: 0.5rem 1rem;
  border: 2px solid #fbbf24;
  border-radius: 0.375rem;
  cursor: pointer;
  transition: all 0.2s;
}

.register-btn:hover {
  background-color: #fbbf24;
  color: black;
}

.login-btn {
  background-color: #eab308;
  color: black;
  font-weight: bold;
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 0.375rem;
  cursor: pointer;
  transition: background-color 0.2s;
}

.login-btn:hover {
  background-color: #ca8a04;
}

/* Hero Section */
.hero-section {
  background: linear-gradient(135deg, #1d4ed8 0%, #1e3a8a 100%);
  color: white;
  padding: 5rem 0;
}

.hero-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1rem;
  text-align: center;
}

.hero-title {
  font-size: 3rem;
  font-weight: bold;
  margin-bottom: 1rem;
  line-height: 1.1;
}

.hero-highlight {
  color: #fbbf24;
}

.hero-description {
  font-size: 1.25rem;
  margin-bottom: 2rem;
  max-width: 42rem;
  margin-left: auto;
  margin-right: auto;
  opacity: 0.9;
  line-height: 1.6;
}

.search-container {
  max-width: 28rem;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.search-input {
  width: 100%;
  padding: 0.75rem 1rem;
  color: black;
  border-radius: 0.5rem;
  border: 1px solid #d1d5db;
  font-size: 1rem;
}

.search-input:focus {
  outline: none;
  ring: 2px solid #fbbf24;
  border-color: transparent;
}

.search-btn {
  background-color: #eab308;
  color: black;
  font-weight: bold;
  padding: 0.75rem 2rem;
  border: none;
  border-radius: 0.5rem;
  cursor: pointer;
  transition: background-color 0.2s;
  font-size: 1rem;
}

.search-btn:hover {
  background-color: #ca8a04;
}

/* Features Section */
.features-section {
  padding: 4rem 0;
  background-color: #f9fafb;
}

.features-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1rem;
}

.section-header {
  text-align: center;
  margin-bottom: 3rem;
}

.section-title {
  font-size: 2.25rem;
  font-weight: bold;
  color: #1f2937;
  margin: 0;
}

.title-highlight {
  color: #eab308;
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1.5rem;
}

.feature-card {
  background-color: #1d4ed8;
  color: white;
  padding: 1.5rem;
  border-radius: 0.5rem;
  text-align: center;
  cursor: pointer;
  transition: transform 0.3s, box-shadow 0.3s;
  box-shadow: 0 10px 15px rgba(0, 0, 0, 0.1);
}

.feature-card:hover {
  transform: scale(1.05);
  box-shadow: 0 20px 25px rgba(0, 0, 0, 0.15);
}

.feature-icon {
  height: 4rem;
  width: 4rem;
  margin: 0 auto 1rem;
  color: #fbbf24;
}

.feature-title {
  font-size: 1.25rem;
  font-weight: bold;
  margin-bottom: 0.75rem;
}

.feature-description {
  font-size: 0.875rem;
  opacity: 0.9;
  line-height: 1.5;
}

/* Mission Section */
.mission-section {
  background: linear-gradient(135deg, #1e40af 0%, #1e3a8a 100%);
  color: white;
  padding: 4rem 0;
}

.mission-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1rem;
}

.mission-title {
  font-size: 2.25rem;
  font-weight: bold;
  margin: 0;
  text-align: center;
  margin-bottom: 3rem;
}

.title-highlight-yellow {
  color: #fbbf24;
}

.mission-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 3rem;
  align-items: center;
}

@media (min-width: 1024px) {
  .mission-grid {
    grid-template-columns: 1fr 1fr;
  }
}

.mission-image-container {
  order: 2;
}

@media (min-width: 1024px) {
  .mission-image-container {
    order: 1;
  }
}

.mission-image {
  width: 100%;
  height: 20rem;
  object-fit: cover;
  border-radius: 0.5rem;
  box-shadow: 0 10px 15px rgba(0, 0, 0, 0.1);
}

.mission-text {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  order: 1;
}

@media (min-width: 1024px) {
  .mission-text {
    order: 2;
  }
}

.mission-item {
  margin-bottom: 1.5rem;
}

.mission-subtitle {
  font-size: 1.5rem;
  font-weight: bold;
  margin-bottom: 1rem;
  color: #fbbf24;
}

.mission-description {
  font-size: 1.125rem;
  opacity: 0.9;
  line-height: 1.6;
}

/* Team Section */
.team-section {
  padding: 4rem 0;
  background-color: #f9fafb;
}

.team-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1rem;
}

.team-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  max-width: 64rem;
  margin: 0 auto;
}

.team-card {
  background-color: white;
  padding: 1.5rem;
  border-radius: 0.5rem;
  text-align: center;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: box-shadow 0.3s;
}

.team-card:hover {
  box-shadow: 0 10px 15px rgba(0, 0, 0, 0.1);
}

.team-image {
  width: 8rem;
  height: 8rem;
  border-radius: 50%;
  margin: 0 auto 1rem;
  object-fit: cover;
  border: 4px solid #e5e7eb;
}

.team-name {
  font-size: 1.25rem;
  font-weight: bold;
  margin-bottom: 0.5rem;
  color: #1f2937;
}

.team-position {
  color: #1d4ed8;
  font-weight: 600;
  margin-bottom: 0.5rem;
}

.team-description {
  color: #6b7280;
  font-size: 0.875rem;
  line-height: 1.5;
}

/* Footer Section */
.footer-section {
  background: linear-gradient(135deg, #1e3a8a 0%, #1e40af 100%);
  color: white;
  padding: 4rem 0;
}

.footer-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1rem;
  text-align: center;
}

.footer-title {
  font-size: 2.25rem;
  font-weight: bold;
  margin-bottom: 1.5rem;
  line-height: 1.2;
}

@media (min-width: 768px) {
  .footer-title {
    font-size: 3rem;
  }
}

.cta-btn {
  background-color: #eab308;
  color: black;
  font-weight: bold;
  padding: 1rem 2rem;
  font-size: 1.125rem;
  border: none;
  border-radius: 0.5rem;
  cursor: pointer;
  transition: background-color 0.2s, box-shadow 0.2s;
  box-shadow: 0 10px 15px rgba(0, 0, 0, 0.1);
}

.cta-btn:hover {
  background-color: #ca8a04;
  box-shadow: 0 20px 25px rgba(0, 0, 0, 0.15);
}

/* Dashboard Styles */
.dashboard-container {
  min-height: 100vh;
  background-color: #f8fafc;
}

.dashboard-header {
  background-color: #2563eb;
  color: white;
}

.dashboard-header-content {
  max-width: 1400px;
  margin: 0 auto;
  padding: 1rem 2rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.dashboard-brand {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.dashboard-shield-icon {
  height: 2.5rem;
  width: 2.5rem;
  color: #fbbf24;
}

.dashboard-brand-title {
  font-size: 1.25rem;
  font-weight: bold;
  margin: 0;
}

.dashboard-brand-subtitle {
  font-size: 0.875rem;
  opacity: 0.9;
  margin: 0;
}

.dashboard-header-right {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.dashboard-time {
  font-size: 0.875rem;
  opacity: 0.9;
}

.dashboard-search {
  padding: 0.5rem 1rem;
  border-radius: 0.375rem;
  border: 1px solid #d1d5db;
  color: black;
}

.dashboard-nav {
  background-color: #1d4ed8;
  padding: 0 2rem;
  display: flex;
  gap: 0.5rem;
  max-width: 1400px;
  margin: 0 auto;
}

.nav-item {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 1rem;
  background: none;
  border: none;
  color: white;
  cursor: pointer;
  transition: background-color 0.2s;
  border-radius: 0.375rem 0.375rem 0 0;
}

.nav-item:hover {
  background-color: rgba(255, 255, 255, 0.1);
}

.nav-item.active {
  background-color: #f8fafc;
  color: #1f2937;
}

.nav-icon {
  height: 1rem;
  width: 1rem;
}

.logout-btn {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 1rem;
  background: none;
  border: none;
  color: white;
  cursor: pointer;
  transition: background-color 0.2s;
  border-radius: 0.375rem;
  margin-left: auto;
}

.logout-btn:hover {
  background-color: rgba(255, 255, 255, 0.1);
}

.dashboard-main {
  max-width: 1400px;
  margin: 0 auto;
  padding: 2rem;
}

.dashboard-content {
  background-color: white;
  border-radius: 0.5rem;
  padding: 2rem;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.dashboard-title-section {
  margin-bottom: 2rem;
}

.dashboard-title {
  font-size: 2rem;
  font-weight: bold;
  color: #1f2937;
  margin-bottom: 0.5rem;
}

.dashboard-subtitle {
  color: #6b7280;
  font-size: 1rem;
}

.dashboard-controls {
  margin-bottom: 2rem;
}

.search-filter-container {
  display: flex;
  gap: 1rem;
  align-items: center;
}

.search-box {
  position: relative;
  flex: 1;
  max-width: 400px;
}

.search-icon {
  position: absolute;
  left: 0.75rem;
  top: 50%;
  transform: translateY(-50%);
  height: 1rem;
  width: 1rem;
  color: #9ca3af;
}

.search-input-dashboard {
  width: 100%;
  padding: 0.75rem 0.75rem 0.75rem 2.5rem;
  border: 1px solid #d1d5db;
  border-radius: 0.375rem;
  font-size: 0.875rem;
}

.search-input-dashboard:focus {
  outline: none;
  border-color: #2563eb;
  box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
}

.status-filter {
  padding: 0.75rem 1rem;
  border: 1px solid #d1d5db;
  border-radius: 0.375rem;
  font-size: 0.875rem;
  background-color: white;
}

.cases-container {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  margin-bottom: 2rem;
}

.case-card {
  border: 1px solid #e5e7eb;
  border-radius: 0.5rem;
  padding: 1.5rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: white;
  transition: box-shadow 0.2s;
}

.case-card:hover {
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.case-info {
  flex: 1;
}

.case-header {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 1rem;
}

.case-label {
  font-size: 0.75rem;
  color: #6b7280;
  margin-bottom: 0.25rem;
  text-transform: uppercase;
  font-weight: 500;
}

.case-id {
  font-size: 1rem;
  font-weight: bold;
  color: #2563eb;
  margin: 0;
}

.case-value {
  font-size: 0.875rem;
  color: #1f2937;
  margin: 0;
}

.case-actions {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.status-badge {
  padding: 0.25rem 0.75rem;
  border-radius: 9999px;
  font-size: 0.75rem;
  font-weight: 600;
  text-transform: uppercase;
}

.status-badge.resolved {
  background-color: #dcfce7;
  color: #166534;
}

.status-badge.pending {
  background-color: #fef3c7;
  color: #92400e;
}

.status-badge.in-progress {
  background-color: #dbeafe;
  color: #1e40af;
}

.view-more-btn {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.5rem 1rem;
  background-color: #2563eb;
  color: white;
  border: none;
  border-radius: 0.375rem;
  cursor: pointer;
  font-size: 0.875rem;
  transition: background-color 0.2s;
}

.view-more-btn:hover {
  background-color: #1d4ed8;
}

.view-icon {
  height: 1rem;
  width: 1rem;
}

.pagination {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: 1rem;
  border-top: 1px solid #e5e7eb;
}

.pagination-info {
  color: #6b7280;
  font-size: 0.875rem;
}

.pagination-controls {
  display: flex;
  gap: 0.5rem;
}

.pagination-btn {
  padding: 0.5rem 0.75rem;
  border: 1px solid #d1d5db;
  background-color: white;
  color: #374151;
  border-radius: 0.375rem;
  cursor: pointer;
  font-size: 0.875rem;
  transition: all 0.2s;
}

.pagination-btn:hover:not(:disabled) {
  background-color: #f3f4f6;
}

.pagination-btn.active {
  background-color: #2563eb;
  color: white;
  border-color: #2563eb;
}

.pagination-btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

/* Modal Styles */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.modal-content {
  background-color: white;
  padding: 2rem;
  border-radius: 0.5rem;
  width: 90%;
  max-width: 400px;
  box-shadow: 0 20px 25px rgba(0, 0, 0, 0.15);
}

.modal-title {
  font-size: 1.5rem;
  font-weight: bold;
  margin-bottom: 1.5rem;
  text-align: center;
  color: #1f2937;
}

.form-group {
  margin-bottom: 1rem;
}

.form-group label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: 500;
  color: #374151;
}

.form-input {
  width: 100%;
  padding: 0.75rem;
  border: 1px solid #d1d5db;
  border-radius: 0.375rem;
  font-size: 1rem;
}

.form-input:focus {
  outline: none;
  border-color: #2563eb;
  box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
}

.modal-actions {
  display: flex;
  gap: 1rem;
  margin-top: 1.5rem;
}

.cancel-btn {
  flex: 1;
  padding: 0.75rem;
  border: 1px solid #d1d5db;
  background-color: white;
  color: #374151;
  border-radius: 0.375rem;
  cursor: pointer;
  font-weight: 500;
  transition: background-color 0.2s;
}

.cancel-btn:hover {
  background-color: #f3f4f6;
}

.submit-btn {
  flex: 1;
  padding: 0.75rem;
  background-color: #2563eb;
  color: white;
  border: none;
  border-radius: 0.375rem;
  cursor: pointer;
  font-weight: 500;
  transition: background-color 0.2s;
}

.submit-btn:hover {
  background-color: #1d4ed8;
}

/* Responsive Design */
@media (min-width: 640px) {
  .search-container {
    flex-direction: row;
    align-items: center;
  }
  
  .search-btn {
    width: auto;
  }
}

@media (min-width: 768px) {
  .hero-title {
    font-size: 4rem;
  }
  
  .features-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1024px) {
  .features-grid {
    grid-template-columns: repeat(4, 1fr);
  }
  
  .team-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}
</style>