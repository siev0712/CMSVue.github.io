<template>
  <div class="page-container">
    <!-- Landing Page -->
    <div v-if="!isLoggedIn">
      <!-- Header -->
      <header class="header">
        <div class="header-content">
          <div class="header-brand">
            <div class="logo-container">
              <ShieldIcon class="shield-icon" />
              <div class="logo-glow"></div>
            </div>
            <div>
              <h1 class="brand-title">BARANGAY TALAMBAN</h1>
              <p class="brand-subtitle">Official Digital Portal</p>
            </div>
          </div>
          <div class="auth-buttons">
            <button @click="showRegisterModal = true" class="register-btn">
              <span>REGISTER</span>
              <div class="btn-shine"></div>
            </button>
            <button @click="showLoginModal = true" class="login-btn">
              <span>LOGIN</span>
              <div class="btn-shine"></div>
            </button>
          </div>
        </div>
      </header>

      <!-- Hero Section -->
      <section class="hero-section">
        <div class="hero-background">
          <div class="hero-pattern"></div>
          <div class="floating-shapes">
            <div class="shape shape-1"></div>
            <div class="shape shape-2"></div>
            <div class="shape shape-3"></div>
          </div>
        </div>
        <div class="hero-content">
          <div class="hero-badge">
            <span>🏛️ Official Government Portal</span>
          </div>
          <h2 class="hero-title">
            Welcome to<br />
            <span class="hero-highlight">Barangay Talamban</span>
          </h2>
          <p class="hero-description">
            Experience seamless digital governance with our comprehensive community services platform. 
            Connect, engage, and thrive in our progressive barangay.
          </p>
          <div class="search-container">
            <div class="search-wrapper">
              <Search class="search-icon" />
              <input 
                type="text"
                placeholder="Search services, announcements, or information..."
                class="search-input"
              />
              <button class="search-btn">
                <span>SEARCH</span>
                <div class="btn-glow"></div>
              </button>
            </div>
          </div>
        </div>
      </section>

      <!-- Features Section -->
      <section class="features-section">
        <div class="features-content">
          <div class="section-header">
            <div class="section-badge">✨ Our Services</div>
            <h3 class="section-title">
              Empowering <span class="title-highlight">Digital Solutions</span>
            </h3>
            <p class="section-description">
              Discover our comprehensive suite of digital services designed to make your barangay experience seamless and efficient.
            </p>
          </div>
          <div class="features-grid">
            <div 
              v-for="(feature, index) in features"
              :key="index"
              class="feature-card"
              :style="{ animationDelay: `${index * 0.1}s` }"
            >
              <div class="feature-icon-wrapper">
                <component :is="feature.icon" class="feature-icon" />
                <div class="icon-glow"></div>
              </div>
              <h4 class="feature-title">{{ feature.title }}</h4>
              <p class="feature-description">{{ feature.description }}</p>
              <div class="feature-arrow">→</div>
            </div>
          </div>
        </div>
      </section>

      <!-- Mission & Vision Section -->
      <section class="mission-section">
        <div class="mission-background">
          <div class="mission-pattern"></div>
        </div>
        <div class="mission-content">
          <div class="section-header">
            <div class="section-badge light">🎯 Our Purpose</div>
            <h3 class="mission-title">
              Mission & <span class="title-highlight-yellow">Vision</span>
            </h3>
          </div>
          <div class="mission-grid">
            <div class="mission-image-container">
              <div class="image-frame">
                <img 
                  src="./placeholder.svg?height=400&width=600"
                  alt="Barangay Building"
                  class="mission-image"
                />
                <div class="image-overlay"></div>
              </div>
            </div>
            <div class="mission-text">
              <div class="mission-item">
                <div class="mission-icon">🎯</div>
                <h4 class="mission-subtitle">Our Mission</h4>
                <p class="mission-description">
                  To provide efficient, transparent, and responsive governance that promotes the welfare and development of our community while preserving our cultural heritage and environmental sustainability.
                </p>
              </div>
              <div class="mission-item">
                <div class="mission-icon">🌟</div>
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
            <div class="section-badge">👥 Leadership</div>
            <h3 class="section-title">
              Meet Our <span class="title-highlight">Dedicated Team</span>
            </h3>
            <p class="section-description">
              Our committed leaders working tirelessly to serve and uplift our community.
            </p>
          </div>
          <div class="team-grid">
            <div 
              v-for="(member, index) in teamMembers"
              :key="index"
              class="team-card"
              :style="{ animationDelay: `${index * 0.2}s` }"
            >
              <div class="team-image-wrapper">
                <img 
                  :src="member.image"
                  :alt="member.name"
                  class="team-image"
                />
                <div class="image-border"></div>
              </div>
              <div class="team-info">
                <h4 class="team-name">{{ member.name }}</h4>
                <p class="team-position">{{ member.position }}</p>
                <p class="team-description">{{ member.description }}</p>
              </div>
              <div class="team-social">
                <div class="social-link">📧</div>
                <div class="social-link">📞</div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- Footer CTA Section -->
      <section class="footer-section">
        <div class="footer-background">
          <div class="footer-pattern"></div>
        </div>
        <div class="footer-content">
          <div class="cta-badge">🚀 Get Started</div>
          <h3 class="footer-title">
            Report, Manage, Resolve,<br />
            <span class="footer-highlight">All in One Place.</span>
          </h3>
          <p class="footer-description">
            Join thousands of residents already using our digital platform for seamless community services.
          </p>
          <button class="cta-btn">
            <span>GET STARTED TODAY</span>
            <div class="btn-glow"></div>
          </button>
        </div>
      </section>
    </div>

    <!-- Dashboard -->
    <div v-if="isLoggedIn" class="dashboard-container">
      <!-- Dashboard Header -->
      <header class="dashboard-header">
        <div class="dashboard-header-content">
          <div class="dashboard-brand">
            <div class="brand-logo">
              <span>BT</span>
              <div class="logo-pulse"></div>
            </div>
            <div>
              <h1 class="dashboard-brand-title">BARANGAY TALAMBAN</h1>
              <p class="dashboard-brand-subtitle">Case Management System</p>
            </div>
          </div>
          <div class="dashboard-header-right">
            <div class="time-widget">
              <div class="time-icon">🕐</div>
              <div class="time-info">
                <span class="time-label">Philippine Standard Time</span>
                <span class="time-value">{{ currentDateTime }}</span>
              </div>
            </div>
            <div class="search-widget">
              <Search class="search-icon" />
              <input type="search" placeholder="Search..." class="dashboard-search" />
            </div>
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
            <span>{{ item.name }}</span>
            <div class="nav-indicator"></div>
          </button>
          <button @click="logout" class="logout-btn">
            <LogOut class="nav-icon" />
            <span>Logout</span>
          </button>
        </nav>
      </header>

      <!-- Dashboard Content -->
      <main class="dashboard-main">
        <!-- Dashboard Page -->
        <div v-if="activeNav === 'Dashboard'" class="dashboard-content">
          <div class="dashboard-title-section">
            <div class="title-wrapper">
              <h2 class="dashboard-title">
                <span class="title-icon">📊</span>
                Dashboard Overview
              </h2>
              <p class="dashboard-subtitle">Manage and track your barangay cases and complaints</p>
            </div>
            <div class="stats-cards">
              <div class="stat-card">
                <div class="stat-icon">📋</div>
                <div class="stat-info">
                  <span class="stat-number">{{ totalCases }}</span>
                  <span class="stat-label">Total Cases</span>
                </div>
              </div>
              <div class="stat-card">
                <div class="stat-icon">✅</div>
                <div class="stat-info">
                  <span class="stat-number">8</span>
                  <span class="stat-label">Resolved</span>
                </div>
              </div>
              <div class="stat-card">
                <div class="stat-icon">⏳</div>
                <div class="stat-info">
                  <span class="stat-number">4</span>
                  <span class="stat-label">Pending</span>
                </div>
              </div>
            </div>
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
                  <div class="case-field">
                    <p class="case-label">Case ID</p>
                    <p class="case-id">{{ case_item.id }}</p>
                  </div>
                  <div class="case-field">
                    <p class="case-label">Complaint Type</p>
                    <p class="case-value">{{ case_item.type }}</p>
                  </div>
                  <div class="case-field">
                    <p class="case-label">Respondent</p>
                    <p class="case-value">{{ case_item.respondent }}</p>
                  </div>
                  <div class="case-field">
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
                  <span>View Details</span>
                </button>
              </div>
            </div>
          </div>

          <div class="pagination">
            <p class="pagination-info">Showing {{ startIndex }} to {{ endIndex }} of {{ totalCases }} results</p>
            <div class="pagination-controls">
              <button :disabled="currentPage === 1" @click="currentPage--" class="pagination-btn">
                <ChevronLeft class="btn-icon" />
                Previous
              </button>
              <button 
                v-for="page in totalPages" 
                :key="page"
                :class="['pagination-btn', { active: currentPage === page }]"
                @click="currentPage = page"
              >
                {{ page }}
              </button>
              <button :disabled="currentPage === totalPages" @click="currentPage++" class="pagination-btn">
                Next
                <ChevronRight class="btn-icon" />
              </button>
            </div>
          </div>
        </div>

        <!-- File a Complaint Page -->
        <div v-if="activeNav === 'File a Complaint'" class="dashboard-content">
          <div class="dashboard-title-section">
            <div class="title-wrapper">
              <h2 class="dashboard-title">
                <span class="title-icon">📝</span>
                File a Complaint
              </h2>
              <p class="dashboard-subtitle">Submit your complaint details and supporting documents</p>
            </div>
          </div>

          <form @submit.prevent="submitComplaint" class="complaint-form">
            <div class="form-sections">
              <div class="form-section">
                <div class="section-header-form">
                  <div class="section-icon">👤</div>
                  <h3 class="section-title-form">Respondent Information</h3>
                </div>
                <div class="form-grid">
                  <div class="form-group">
                    <label>First Name</label>
                    <input v-model="complaintForm.firstName" type="text" placeholder="Enter first name" class="form-input" required />
                  </div>
                  <div class="form-group">
                    <label>Last Name</label>
                    <input v-model="complaintForm.lastName" type="text" placeholder="Enter last name" class="form-input" required />
                  </div>
                  <div class="form-group">
                    <label>Middle Name</label>
                    <input v-model="complaintForm.middleName" type="text" placeholder="Enter middle name" class="form-input" />
                  </div>
                  <div class="form-group">
                    <label>Suffix</label>
                    <input v-model="complaintForm.suffix" type="text" placeholder="Jr., Sr., III" class="form-input" />
                  </div>
                  <div class="form-group">
                    <label>Sitio/Purok/Subdivision</label>
                    <select v-model="complaintForm.sitio" class="form-select">
                      <option value="">Select location</option>
                      <option value="Sitio 1">Sitio 1</option>
                      <option value="Sitio 2">Sitio 2</option>
                      <option value="Purok 1">Purok 1</option>
                      <option value="Purok 2">Purok 2</option>
                    </select>
                  </div>
                  <div class="form-group">
                    <label>House No. & Street</label>
                    <input v-model="complaintForm.address" type="text" placeholder="Complete address" class="form-input" required />
                  </div>
                </div>
                <div class="form-note">
                  <span class="note-icon">ℹ️</span>
                  Respondent must be from Barangay Talamban
                </div>
              </div>

              <div class="form-section">
                <div class="section-header-form">
                  <div class="section-icon">📄</div>
                  <h3 class="section-title-form">Complaint Details</h3>
                </div>
                <div class="form-group">
                  <label>Complaint Description</label>
                  <textarea 
                    v-model="complaintForm.description" 
                    placeholder="Describe your complaint in detail..." 
                    class="form-textarea"
                    rows="8"
                    maxlength="500"
                    required
                  ></textarea>
                  <div class="character-count">
                    <span :class="{ 'text-warning': complaintForm.description.length > 400 }">
                      {{ complaintForm.description.length }}/500 Characters
                    </span>
                  </div>
                </div>

                <div class="upload-section">
                  <div class="section-header-form">
                    <div class="section-icon">📎</div>
                    <h3 class="section-title-form">Supporting Documents</h3>
                  </div>
                  <div class="upload-area">
                    <Upload class="upload-icon" />
                    <h4>Drag & drop files here</h4>
                    <p>or</p>
                    <button type="button" class="upload-btn">
                      <span>Choose Files</span>
                    </button>
                    <p class="upload-note">
                      <span class="note-icon">💡</span>
                      Supported formats: PDF, JPG, PNG (Max 10MB)
                    </p>
                  </div>
                </div>
              </div>
            </div>

            <div class="form-actions">
              <button type="submit" class="proceed-btn">
                <span>Proceed to Payment</span>
                <div class="btn-glow"></div>
              </button>
              <div class="privacy-note">
                <span class="privacy-icon">🔒</span>
                By submitting, you consent to the collection and processing of your data in compliance with our 
                <a href="#" class="privacy-link">Privacy Policy</a> and <a href="#" class="privacy-link">Data Privacy Act</a>.
              </div>
            </div>
          </form>
        </div>

        <!-- Calendar Page -->
        <div v-if="activeNav === 'Calendar'" class="dashboard-content">
          <div class="dashboard-title-section">
            <div class="title-wrapper">
              <h2 class="dashboard-title">
                <span class="title-icon">📅</span>
                Calendar & Hearings
              </h2>
              <p class="dashboard-subtitle">View scheduled hearings and important dates</p>
            </div>
          </div>

          <div class="calendar-layout">
            <div class="calendar-main">
              <div class="calendar-header">
                <button @click="previousMonth" class="calendar-nav-btn">
                  <ChevronLeft class="nav-icon" />
                </button>
                <h3 class="calendar-month">{{ currentMonthYear }}</h3>
                <button @click="nextMonth" class="calendar-nav-btn">
                  <ChevronRight class="nav-icon" />
                </button>
              </div>

              <div class="calendar-grid">
                <div class="calendar-day-header" v-for="day in dayHeaders" :key="day">{{ day }}</div>
                <div 
                  v-for="date in calendarDates" 
                  :key="date.date"
                  :class="['calendar-day', { 'other-month': !date.currentMonth, 'has-event': date.hasEvent, 'today': isToday(date.date) }]"
                >
                  <span class="day-number">{{ date.day }}</span>
                  <div v-if="date.events" class="day-events">
                    <div 
                      v-for="event in date.events" 
                      :key="event.id"
                      :class="['event-bar', event.type]"
                    ></div>
                  </div>
                </div>
              </div>
            </div>

            <div class="calendar-sidebar">
              <div class="sidebar-header">
                <h3 class="sidebar-title">
                  <span class="sidebar-icon">⚖️</span>
                  Scheduled Hearings
                </h3>
              </div>
              <div class="hearings-list">
                <div v-for="hearing in scheduledHearings" :key="hearing.id" class="hearing-card">
                  <div class="hearing-info">
                    <h4 class="hearing-case">{{ hearing.caseId }}</h4>
                    <p class="hearing-type">
                      <span class="type-icon">📋</span>
                      {{ hearing.type }}
                    </p>
                    <p class="hearing-respondent">
                      <span class="respondent-icon">👤</span>
                      {{ hearing.respondent }}
                    </p>
                  </div>
                  <div class="hearing-actions">
                    <span :class="['status-badge', hearing.status.toLowerCase().replace(' ', '-')]">
                      {{ hearing.status }}
                    </span>
                    <button class="view-more-btn">
                      <Eye class="view-icon" />
                      View Details
                    </button>
                  </div>
                </div>
              </div>
              <button @click="activeNav = 'File a Complaint'" class="file-complaint-btn">
                <span class="btn-icon">➕</span>
                File New Complaint
              </button>
            </div>
          </div>
        </div>

        <!-- Profile Page -->
        <div v-if="activeNav === 'Profile'" class="dashboard-content">
          <div class="profile-layout">
            <div class="profile-main">
              <div class="profile-header">
                <div class="profile-title-section">
                  <h2 class="profile-title">
                    <span class="title-icon">👤</span>
                    User Profile
                  </h2>
                  <p class="profile-subtitle">Manage your personal information and account settings</p>
                </div>
                <button @click="editMode = !editMode" class="edit-profile-btn">
                  <Edit class="edit-icon" />
                  <span>{{ editMode ? 'Cancel Edit' : 'Edit Profile' }}</span>
                </button>
              </div>

              <form @submit.prevent="saveProfile" class="profile-form">
                <div class="profile-section">
                  <div class="section-header-form">
                    <div class="section-icon">🆔</div>
                    <h3 class="profile-section-title">Personal Information</h3>
                  </div>
                  <div class="profile-grid">
                    <div class="form-group">
                      <label>First Name</label>
                      <input 
                        v-model="userProfile.firstName" 
                        type="text" 
                        :disabled="!editMode"
                        class="form-input"
                      />
                    </div>
                    <div class="form-group">
                      <label>Last Name</label>
                      <input 
                        v-model="userProfile.lastName" 
                        type="text" 
                        :disabled="!editMode"
                        class="form-input"
                      />
                    </div>
                    <div class="form-group">
                      <label>Middle Name</label>
                      <input 
                        v-model="userProfile.middleName" 
                        type="text" 
                        :disabled="!editMode"
                        placeholder="Middle Name"
                        class="form-input"
                      />
                    </div>
                    <div class="form-group">
                      <label>Date of Birth</label>
                      <input 
                        v-model="userProfile.dateOfBirth" 
                        type="date" 
                        :disabled="!editMode"
                        class="form-input"
                      />
                    </div>
                    <div class="form-group">
                      <label>Suffix</label>
                      <select v-model="userProfile.suffix" :disabled="!editMode" class="form-select">
                        <option value="">Select Suffix</option>
                        <option value="Jr.">Jr.</option>
                        <option value="Sr.">Sr.</option>
                        <option value="III">III</option>
                      </select>
                    </div>
                    <div class="form-group">
                      <label>Sex</label>
                      <select v-model="userProfile.sex" :disabled="!editMode" class="form-select">
                        <option value="">Select Sex</option>
                        <option value="Male">Male</option>
                        <option value="Female">Female</option>
                      </select>
                    </div>
                  </div>
                </div>

                <div class="profile-section">
                  <div class="section-header-form">
                    <div class="section-icon">🏠</div>
                    <h3 class="profile-section-title">Address Information</h3>
                  </div>
                  <div class="profile-grid">
                    <div class="form-group">
                      <label>Country</label>
                      <input 
                        v-model="userProfile.country" 
                        type="text" 
                        :disabled="!editMode"
                        class="form-input"
                      />
                    </div>
                    <div class="form-group">
                      <label>Province</label>
                      <input 
                        v-model="userProfile.province" 
                        type="text" 
                        :disabled="!editMode"
                        placeholder="Province"
                        class="form-input"
                      />
                    </div>
                    <div class="form-group">
                      <label>City/Municipality</label>
                      <input 
                        v-model="userProfile.city" 
                        type="text" 
                        :disabled="!editMode"
                        placeholder="City/Municipality"
                        class="form-input"
                      />
                    </div>
                    <div class="form-group">
                      <label>Barangay</label>
                      <input 
                        v-model="userProfile.barangay" 
                        type="text" 
                        :disabled="!editMode"
                        class="form-input"
                      />
                    </div>
                    <div class="form-group">
                      <label>Sitio/Purok/Subdivision</label>
                      <input 
                        v-model="userProfile.sitio" 
                        type="text" 
                        :disabled="!editMode"
                        placeholder="Sitio/Purok/Subd."
                        class="form-input"
                      />
                    </div>
                    <div class="form-group">
                      <label>House No. & Street</label>
                      <input 
                        v-model="userProfile.address" 
                        type="text" 
                        :disabled="!editMode"
                        placeholder="House No. & Street"
                        class="form-input"
                      />
                    </div>
                    <div class="form-group">
                      <label>Email Address</label>
                      <input 
                        v-model="userProfile.email" 
                        type="email" 
                        :disabled="!editMode"
                        placeholder="Email"
                        class="form-input"
                      />
                    </div>
                    <div class="form-group">
                      <label>Phone Number</label>
                      <input 
                        v-model="userProfile.phone" 
                        type="tel" 
                        :disabled="!editMode"
                        placeholder="+63"
                        class="form-input"
                      />
                    </div>
                  </div>
                </div>

                <div v-if="editMode" class="profile-actions">
                  <button type="submit" class="save-btn">
                    <CheckCircle class="btn-icon" />
                    <span>Save Changes</span>
                  </button>
                </div>
              </form>

              <div class="profile-status">
                <div class="status-indicator">
                  <CheckCircle class="status-icon" />
                  <span>Profile information is up to date</span>
                </div>
              </div>
            </div>

            <div class="profile-sidebar">
              <div class="profile-avatar">
                <div class="avatar-circle">
                  <User class="avatar-icon" />
                  <div class="avatar-status"></div>
                </div>
                <h3 class="profile-name">{{ userProfile.firstName }} {{ userProfile.lastName }}</h3>
                <p class="profile-role">Resident</p>
              </div>

              <nav class="profile-nav">
                <a href="#" class="profile-nav-item">
                  <span class="nav-icon">🔔</span>
                  Notifications
                  <span class="nav-badge">3</span>
                </a>
                <a href="#" class="profile-nav-item">
                  <span class="nav-icon">📋</span>
                  My Cases
                </a>
                <a href="#" class="profile-nav-item active">
                  <span class="nav-icon">👤</span>
                  Profile
                </a>
                <a href="#" class="profile-nav-item">
                  <span class="nav-icon">⚙️</span>
                  Settings
                </a>
              </nav>

              <button @click="logout" class="profile-logout-btn">
                <LogOut class="logout-icon" />
                <span>Log Out</span>
              </button>
            </div>
          </div>
        </div>
      </main>
    </div>

    <!-- Enhanced Login Modal -->
    <div v-if="showLoginModal" class="modal-overlay" @click="showLoginModal = false">
      <div class="modal-content" @click.stop>
        <div class="modal-header">
          <div class="modal-icon">🔐</div>
          <h3 class="modal-title">Welcome Back</h3>
          <p class="modal-subtitle">Sign in to your account</p>
        </div>
        <form @submit.prevent="handleLogin">
          <div class="form-group">
            <label>Email or Username</label>
            <input v-model="loginForm.email" type="text" required class="form-input" placeholder="Enter your email" />
          </div>
          <div class="form-group">
            <label>Password</label>
            <input v-model="loginForm.password" type="password" required class="form-input" placeholder="Enter your password" />
          </div>
          <div class="modal-actions">
            <button type="button" @click="showLoginModal = false" class="cancel-btn">Cancel</button>
            <button type="submit" class="submit-btn">
              <span>Sign In</span>
              <div class="btn-glow"></div>
            </button>
          </div>
        </form>
      </div>
    </div>

    <!-- Enhanced Register Modal -->
    <div v-if="showRegisterModal" class="modal-overlay" @click="showRegisterModal = false">
      <div class="modal-content" @click.stop>
        <div class="modal-header">
          <div class="modal-icon">✨</div>
          <h3 class="modal-title">Join Our Community</h3>
          <p class="modal-subtitle">Create your account</p>
        </div>
        <form @submit.prevent="handleRegister">
          <div class="form-group">
            <label>Full Name</label>
            <input v-model="registerForm.fullName" type="text" required class="form-input" placeholder="Enter your full name" />
          </div>
          <div class="form-group">
            <label>Email</label>
            <input v-model="registerForm.email" type="email" required class="form-input" placeholder="Enter your email" />
          </div>
          <div class="form-group">
            <label>Password</label>
            <input v-model="registerForm.password" type="password" required class="form-input" placeholder="Create a password" />
          </div>
          <div class="form-group">
            <label>Confirm Password</label>
            <input v-model="registerForm.confirmPassword" type="password" required class="form-input" placeholder="Confirm your password" />
          </div>
          <div class="modal-actions">
            <button type="button" @click="showRegisterModal = false" class="cancel-btn">Cancel</button>
            <button type="submit" class="submit-btn">
              <span>Create Account</span>
              <div class="btn-glow"></div>
            </button>
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
  Eye,
  Upload,
  ChevronLeft,
  ChevronRight,
  Edit,
  CheckCircle
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
const editMode = ref(false)

// Calendar data
const currentDate = ref(new Date())
const dayHeaders = ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat']

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

const complaintForm = ref({
  firstName: '',
  lastName: '',
  middleName: '',
  suffix: '',
  sitio: '',
  address: '',
  description: ''
})

const userProfile = ref({
  firstName: 'John Steven',
  lastName: 'Sanchez',
  middleName: '',
  dateOfBirth: '',
  suffix: '',
  sex: '',
  country: 'Philippines',
  province: '',
  city: '',
  barangay: 'Talamban',
  sitio: '',
  address: '',
  email: '',
  phone: ''
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

// Scheduled hearings
const scheduledHearings = ref([
  { id: 'Case #0002', type: 'Theft and Robbery', respondent: 'Blasminda Mayol', status: 'RESOLVED' },
  { id: 'Case #0003', type: 'Theft and Robbery', respondent: 'Blasminda Mayol', status: 'ONGOING' }
])

// Features data
const features = [
  {
    icon: FileText,
    title: 'Online Case Filing',
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

const currentMonthYear = computed(() => {
  const options = { year: 'numeric', month: 'long' }
  return currentDate.value.toLocaleDateString('en-US', options).toUpperCase()
})

const calendarDates = computed(() => {
  const year = currentDate.value.getFullYear()
  const month = currentDate.value.getMonth()
  
  const firstDay = new Date(year, month, 1)
  const lastDay = new Date(year, month + 1, 0)
  const startDate = new Date(firstDay)
  startDate.setDate(startDate.getDate() - firstDay.getDay())
  
  const dates = []
  const currentDateObj = new Date(startDate)
  
  for (let i = 0; i < 42; i++) {
    const isCurrentMonth = currentDateObj.getMonth() === month
    const dayNumber = currentDateObj.getDate()
    
    // Add sample events
    let events = null
    if (isCurrentMonth && (dayNumber === 5 || dayNumber === 19)) {
      events = [
        { id: 1, type: dayNumber === 5 ? 'resolved' : 'ongoing' }
      ]
    }
    
    dates.push({
      date: new Date(currentDateObj),
      day: dayNumber,
      currentMonth: isCurrentMonth,
      hasEvent: !!events,
      events: events
    })
    
    currentDateObj.setDate(currentDateObj.getDate() + 1)
  }
  
  return dates
})

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

const isToday = (date) => {
  const today = new Date()
  return date.toDateString() === today.toDateString()
}

const handleLogin = () => {
  if (loginForm.value.email && loginForm.value.password) {
    isLoggedIn.value = true
    showLoginModal.value = false
    loginForm.value = { email: '', password: '' }
  }
}

const handleRegister = () => {
  if (registerForm.value.password !== registerForm.value.confirmPassword) {
    alert('Passwords do not match!')
    return
  }
  
  if (registerForm.value.fullName && registerForm.value.email && registerForm.value.password) {
    alert('Registration successful! Please login.')
    showRegisterModal.value = false
    showLoginModal.value = true
    registerForm.value = { fullName: '', email: '', password: '', confirmPassword: '' }
  }
}

const submitComplaint = () => {
  alert('Complaint submitted successfully!')
  complaintForm.value = {
    firstName: '',
    lastName: '',
    middleName: '',
    suffix: '',
    sitio: '',
    address: '',
    description: ''
  }
}

const saveProfile = () => {
  editMode.value = false
  alert('Profile updated successfully!')
}

const previousMonth = () => {
  currentDate.value = new Date(currentDate.value.getFullYear(), currentDate.value.getMonth() - 1, 1)
}

const nextMonth = () => {
  currentDate.value = new Date(currentDate.value.getFullYear(), currentDate.value.getMonth() + 1, 1)
}

const logout = () => {
  isLoggedIn.value = false
  activeNav.value = 'Dashboard'
  currentPage.value = 1
  searchQuery.value = ''
  statusFilter.value = ''
  editMode.value = false
}

// Lifecycle
onMounted(() => {
  updateDateTime()
  setInterval(updateDateTime, 1000)
})
</script>

<style scoped>
/* Enhanced Base Styles */
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
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
}

.page-container {
  height: 100vh;
  width: 100%;
  margin: 0;
  padding: 0;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  overflow-x: hidden;
}

/* Enhanced Header Styles */
.header {
  background: linear-gradient(135deg, #1e3a8a 0%, #1d4ed8 50%, #2563eb 100%);
  color: white;
  padding: 1.5rem 0;
  position: relative;
  overflow: hidden;
}

.header::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: url("data:image/svg+xml,%3Csvg width='60' height='60' viewBox='0 0 60 60' xmlns='http://www.w3.org/2000/svg'%3E%3Cg fill='none' fill-rule='evenodd'%3E%3Cg fill='%23ffffff' fill-opacity='0.05'%3E%3Ccircle cx='30' cy='30' r='2'/%3E%3C/g%3E%3C/g%3E%3C/svg%3E") repeat;
}

.header-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  position: relative;
  z-index: 2;
}

.header-brand {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.logo-container {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
}

.shield-icon {
  height: 3rem;
  width: 3rem;
  color: #fbbf24;
  filter: drop-shadow(0 4px 8px rgba(251, 191, 36, 0.3));
  z-index: 2;
  position: relative;
}

.logo-glow {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 4rem;
  height: 4rem;
  background: radial-gradient(circle, rgba(251, 191, 36, 0.3) 0%, transparent 70%);
  border-radius: 50%;
  animation: pulse 2s ease-in-out infinite;
}

@keyframes pulse {
  0%, 100% { transform: translate(-50%, -50%) scale(1); opacity: 0.7; }
  50% { transform: translate(-50%, -50%) scale(1.1); opacity: 1; }
}

.brand-title {
  font-size: 1.5rem;
  font-weight: 800;
  margin: 0;
  background: linear-gradient(135deg, #ffffff 0%, #fbbf24 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.brand-subtitle {
  font-size: 0.875rem;
  opacity: 0.9;
  margin: 0;
  font-weight: 500;
}

.auth-buttons {
  display: flex;
  gap: 1rem;
}

.register-btn, .login-btn {
  position: relative;
  overflow: hidden;
  font-weight: 600;
  padding: 0.75rem 1.5rem;
  border-radius: 0.5rem;
  cursor: pointer;
  transition: all 0.3s ease;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.register-btn {
  background: transparent;
  color: white;
  border: 2px solid #fbbf24;
}

.register-btn:hover {
  background: #fbbf24;
  color: #1e3a8a;
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(251, 191, 36, 0.3);
}

.login-btn {
  background: linear-gradient(135deg, #fbbf24 0%, #f59e0b 100%);
  color: #1e3a8a;
  border: none;
  box-shadow: 0 4px 15px rgba(251, 191, 36, 0.3);
}

.login-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(251, 191, 36, 0.4);
}

.btn-shine {
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
  transition: left 0.5s;
}

.register-btn:hover .btn-shine,
.login-btn:hover .btn-shine {
  left: 100%;
}

/* Enhanced Hero Section */
.hero-section {
  position: relative;
  color: white;
  padding: 8rem 0;
  overflow: hidden;
}

.hero-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, #1e3a8a 0%, #1d4ed8 50%, #2563eb 100%);
}

.hero-pattern {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: url("data:image/svg+xml,%3Csvg width='100' height='100' viewBox='0 0 100 100' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M11 18c3.866 0 7-3.134 7-7s-3.134-7-7-7-7 3.134-7 7 3.134 7 7 7zm48 25c3.866 0 7-3.134 7-7s-3.134-7-7-7-7 3.134-7 7 3.134 7 7 7zm-43-7c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zm63 31c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zM34 90c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zm56-76c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zM12 86c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm28-65c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm23-11c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm-6 60c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm29 22c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zM32 63c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm57-13c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm-9-21c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM60 91c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM35 41c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM12 60c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2z' fill='%23ffffff' fill-opacity='0.03' fill-rule='evenodd'/%3E%3C/svg%3E") repeat;
}

.floating-shapes {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  overflow: hidden;
}

.shape {
  position: absolute;
  border-radius: 50%;
  background: rgba(251, 191, 36, 0.1);
  animation: float 6s ease-in-out infinite;
}

.shape-1 {
  width: 100px;
  height: 100px;
  top: 20%;
  left: 10%;
  animation-delay: 0s;
}

.shape-2 {
  width: 150px;
  height: 150px;
  top: 60%;
  right: 15%;
  animation-delay: 2s;
}

.shape-3 {
  width: 80px;
  height: 80px;
  bottom: 20%;
  left: 70%;
  animation-delay: 4s;
}

@keyframes float {
  0%, 100% { transform: translateY(0px) rotate(0deg); }
  33% { transform: translateY(-20px) rotate(120deg); }
  66% { transform: translateY(10px) rotate(240deg); }
}

.hero-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  text-align: center;
  position: relative;
  z-index: 2;
}

.hero-badge {
  display: inline-block;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  padding: 0.5rem 1.5rem;
  border-radius: 2rem;
  font-size: 0.875rem;
  font-weight: 500;
  margin-bottom: 2rem;
  animation: slideInDown 1s ease-out;
}

@keyframes slideInDown {
  from { opacity: 0; transform: translateY(-30px); }
  to { opacity: 1; transform: translateY(0); }
}

.hero-title {
  font-size: 4rem;
  font-weight: 900;
  margin-bottom: 2rem;
  line-height: 1.1;
  animation: slideInUp 1s ease-out 0.2s both;
}

@keyframes slideInUp {
  from { opacity: 0; transform: translateY(30px); }
  to { opacity: 1; transform: translateY(0); }
}

.hero-highlight {
  background: linear-gradient(135deg, #fbbf24 0%, #f59e0b 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  position: relative;
}

.hero-description {
  font-size: 1.25rem;
  margin-bottom: 3rem;
  max-width: 48rem;
  margin-left: auto;
  margin-right: auto;
  opacity: 0.95;
  line-height: 1.7;
  animation: slideInUp 1s ease-out 0.4s both;
}

.search-container {
  max-width: 32rem;
  margin: 0 auto;
  animation: slideInUp 1s ease-out 0.6s both;
}

.search-wrapper {
  position: relative;
  display: flex;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 1rem;
  padding: 0.5rem;
  transition: all 0.3s ease;
}

.search-wrapper:hover {
  background: rgba(255, 255, 255, 0.15);
  transform: translateY(-2px);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
}

.search-icon {
  position: absolute;
  left: 1.5rem;
  top: 50%;
  transform: translateY(-50%);
  height: 1.25rem;
  width: 1.25rem;
  color: rgba(255, 255, 255, 0.7);
  z-index: 2;
}

.search-input {
  flex: 1;
  padding: 1rem 1rem 1rem 3.5rem;
  background: transparent;
  border: none;
  color: white;
  font-size: 1rem;
  border-radius: 0.75rem;
}

.search-input::placeholder {
  color: rgba(255, 255, 255, 0.7);
}

.search-input:focus {
  outline: none;
}

.search-btn {
  position: relative;
  background: linear-gradient(135deg, #fbbf24 0%, #f59e0b 100%);
  color: #1e3a8a;
  font-weight: 700;
  padding: 1rem 2rem;
  border: none;
  border-radius: 0.75rem;
  cursor: pointer;
  transition: all 0.3s ease;
  overflow: hidden;
}

.search-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 25px rgba(251, 191, 36, 0.4);
}

.btn-glow {
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.3), transparent);
  transition: left 0.5s;
}

.search-btn:hover .btn-glow {
  left: 100%;
}

/* Enhanced Features Section */
.features-section {
  padding: 8rem 0;
  background: linear-gradient(135deg, #f8fafc 0%, #e2e8f0 100%);
  position: relative;
}

.features-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

.section-header {
  text-align: center;
  margin-bottom: 4rem;
}

.section-badge {
  display: inline-block;
  background: linear-gradient(135deg, #2563eb 0%, #1d4ed8 100%);
  color: white;
  padding: 0.5rem 1.5rem;
  border-radius: 2rem;
  font-size: 0.875rem;
  font-weight: 600;
  margin-bottom: 1.5rem;
  box-shadow: 0 4px 15px rgba(37, 99, 235, 0.3);
}

.section-title {
  font-size: 3rem;
  font-weight: 900;
  color: #1f2937;
  margin-bottom: 1rem;
  line-height: 1.2;
}

.title-highlight {
  background: linear-gradient(135deg, #2563eb 0%, #1d4ed8 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.section-description {
  font-size: 1.125rem;
  color: #6b7280;
  max-width: 42rem;
  margin: 0 auto;
  line-height: 1.7;
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 2rem;
}

.feature-card {
  background: white;
  padding: 2.5rem;
  border-radius: 1.5rem;
  text-align: center;
  cursor: pointer;
  transition: all 0.4s ease;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
  border: 1px solid rgba(226, 232, 240, 0.8);
  position: relative;
  overflow: hidden;
  animation: fadeInUp 0.6s ease-out forwards;
  opacity: 0;
  transform: translateY(30px);
}

@keyframes fadeInUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.feature-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 25px 50px rgba(37, 99, 235, 0.15);
  border-color: #2563eb;
}

.feature-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 4px;
  background: linear-gradient(135deg, #2563eb 0%, #1d4ed8 100%);
  transform: scaleX(0);
  transition: transform 0.3s ease;
}

.feature-card:hover::before {
  transform: scaleX(1);
}

.feature-icon-wrapper {
  position: relative;
  display: inline-block;
  margin-bottom: 1.5rem;
}

.feature-icon {
  height: 4rem;
  width: 4rem;
  color: #2563eb;
  transition: all 0.3s ease;
}

.feature-card:hover .feature-icon {
  color: #1d4ed8;
  transform: scale(1.1);
}

.icon-glow {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 5rem;
  height: 5rem;
  background: radial-gradient(circle, rgba(37, 99, 235, 0.1) 0%, transparent 70%);
  border-radius: 50%;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.feature-card:hover .icon-glow {
  opacity: 1;
}

.feature-title {
  font-size: 1.5rem;
  font-weight: 700;
  margin-bottom: 1rem;
  color: #1f2937;
}

.feature-description {
  font-size: 1rem;
  color: #6b7280;
  line-height: 1.6;
  margin-bottom: 1.5rem;
}

.feature-arrow {
  font-size: 1.5rem;
  color: #2563eb;
  opacity: 0;
  transform: translateX(-10px);
  transition: all 0.3s ease;
}

.feature-card:hover .feature-arrow {
  opacity: 1;
  transform: translateX(0);
}

/* Enhanced Mission Section */
.mission-section {
  position: relative;
  color: white;
  padding: 8rem 0;
  overflow: hidden;
}

.mission-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, #1e40af 0%, #1e3a8a 50%, #1d4ed8 100%);
}

.mission-pattern {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: url("data:image/svg+xml,%3Csvg width='80' height='80' viewBox='0 0 80 80' xmlns='http://www.w3.org/2000/svg'%3E%3Cg fill='none' fill-rule='evenodd'%3E%3Cg fill='%23ffffff' fill-opacity='0.03'%3E%3Cpath d='M0 0h80v80H0V0zm20 20v40h40V20H20zm20 35a15 15 0 1 1 0-30 15 15 0 0 1 0 30z' /%3E%3C/g%3E%3C/g%3E%3C/svg%3E") repeat;
}

.mission-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  position: relative;
  z-index: 2;
}

.section-badge.light {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  color: white;
}

.mission-title {
  font-size: 3rem;
  font-weight: 900;
  margin: 0;
  text-align: center;
  margin-bottom: 4rem;
  line-height: 1.2;
}

.title-highlight-yellow {
  background: linear-gradient(135deg, #fbbf24 0%, #f59e0b 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.mission-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 4rem;
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

.image-frame {
  position: relative;
  border-radius: 1.5rem;
  overflow: hidden;
  box-shadow: 0 25px 50px rgba(0, 0, 0, 0.2);
}

.mission-image {
  width: 100%;
  height: 25rem;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.image-frame:hover .mission-image {
  transform: scale(1.05);
}

.image-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, rgba(37, 99, 235, 0.1) 0%, rgba(29, 78, 216, 0.1) 100%);
  opacity: 0;
  transition: opacity 0.3s ease;
}

.image-frame:hover .image-overlay {
  opacity: 1;
}

.mission-text {
  display: flex;
  flex-direction: column;
  gap: 2.5rem;
  order: 1;
}

@media (min-width: 1024px) {
  .mission-text {
    order: 2;
  }
}

.mission-item {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  padding: 2rem;
  border-radius: 1.5rem;
  transition: all 0.3s ease;
}

.mission-item:hover {
  background: rgba(255, 255, 255, 0.1);
  transform: translateY(-5px);
}

.mission-icon {
  font-size: 2.5rem;
  margin-bottom: 1rem;
  display: block;
}

.mission-subtitle {
  font-size: 1.75rem;
  font-weight: 700;
  margin-bottom: 1rem;
  color: #fbbf24;
}

.mission-description {
  font-size: 1.125rem;
  opacity: 0.95;
  line-height: 1.7;
}

/* Enhanced Team Section */
.team-section {
  padding: 8rem 0;
  background: linear-gradient(135deg, #f8fafc 0%, #e2e8f0 100%);
}

.team-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

.team-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 2.5rem;
  max-width: 72rem;
  margin: 0 auto;
}

.team-card {
  background: white;
  padding: 2.5rem;
  border-radius: 1.5rem;
  text-align: center;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
  transition: all 0.4s ease;
  border: 1px solid rgba(226, 232, 240, 0.8);
  position: relative;
  overflow: hidden;
  animation: fadeInUp 0.6s ease-out forwards;
  opacity: 0;
  transform: translateY(30px);
}

.team-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 25px 50px rgba(37, 99, 235, 0.15);
}

.team-image-wrapper {
  position: relative;
  display: inline-block;
  margin-bottom: 1.5rem;
}

.team-image {
  width: 10rem;
  height: 10rem;
  border-radius: 50%;
  object-fit: cover;
  transition: all 0.3s ease;
  position: relative;
  z-index: 2;
}

.image-border {
  position: absolute;
  top: -4px;
  left: -4px;
  right: -4px;
  bottom: -4px;
  border-radius: 50%;
  background: linear-gradient(135deg, #2563eb 0%, #1d4ed8 100%);
  opacity: 0;
  transition: opacity 0.3s ease;
}

.team-card:hover .image-border {
  opacity: 1;
}

.team-info {
  margin-bottom: 1.5rem;
}

.team-name {
  font-size: 1.5rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
  color: #1f2937;
}

.team-position {
  color: #2563eb;
  font-weight: 600;
  margin-bottom: 1rem;
  font-size: 1.125rem;
}

.team-description {
  color: #6b7280;
  font-size: 1rem;
  line-height: 1.6;
}

.team-social {
  display: flex;
  justify-content: center;
  gap: 1rem;
}

.social-link {
  width: 2.5rem;
  height: 2.5rem;
  background: #f3f4f6;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s ease;
  font-size: 1.125rem;
}

.social-link:hover {
  background: #2563eb;
  transform: translateY(-2px);
}

/* Enhanced Footer Section */
.footer-section {
  position: relative;
  color: white;
  padding: 8rem 0;
  overflow: hidden;
}

.footer-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, #1e3a8a 0%, #1e40af 50%, #2563eb 100%);
}

.footer-pattern {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: url("data:image/svg+xml,%3Csvg width='120' height='120' viewBox='0 0 120 120' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M9 0h2v20H9V0zm25.134.84l1.732 1-10 17.32-1.732-1 10-17.32zm-2 0l1.732 1-10 17.32-1.732-1 10-17.32zM58.16 4.134l1 1.732-17.32 10-1-1.732 17.32-10zm-2 0l1 1.732-17.32 10-1-1.732 17.32-10zM81.84 4.134l1 1.732-17.32 10-1-1.732 17.32-10zm-2 0l1 1.732-17.32 10-1-1.732 17.32-10zM105.52 4.134l1 1.732-17.32 10-1-1.732 17.32-10zm-2 0l1 1.732-17.32 10-1-1.732 17.32-10z' fill='%23ffffff' fill-opacity='0.02' fill-rule='evenodd'/%3E%3C/svg%3E") repeat;
}

.footer-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  text-align: center;
  position: relative;
  z-index: 2;
}

.cta-badge {
  display: inline-block;
  background: rgba(251, 191, 36, 0.1);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(251, 191, 36, 0.3);
  color: #fbbf24;
  padding: 0.5rem 1.5rem;
  border-radius: 2rem;
  font-size: 0.875rem;
  font-weight: 600;
  margin-bottom: 2rem;
}

.footer-title {
  font-size: 3.5rem;
  font-weight: 900;
  margin-bottom: 1.5rem;
  line-height: 1.2;
}

.footer-highlight {
  background: linear-gradient(135deg, #fbbf24 0%, #f59e0b 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.footer-description {
  font-size: 1.25rem;
  margin-bottom: 3rem;
  opacity: 0.9;
  max-width: 36rem;
  margin-left: auto;
  margin-right: auto;
  line-height: 1.6;
}

.cta-btn {
  position: relative;
  background: linear-gradient(135deg, #fbbf24 0%, #f59e0b 100%);
  color: #1e3a8a;
  font-weight: 700;
  padding: 1.25rem 3rem;
  font-size: 1.125rem;
  border: none;
  border-radius: 1rem;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 10px 25px rgba(251, 191, 36, 0.3);
  overflow: hidden;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.cta-btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 20px 40px rgba(251, 191, 36, 0.4);
}

/* Enhanced Dashboard Styles */
.dashboard-container {
  min-height: 100vh;
  background: linear-gradient(135deg, #f8fafc 0%, #e2e8f0 100%);
}

.dashboard-header {
  background: linear-gradient(135deg, #1e3a8a 0%, #2563eb 100%);
  color: white;
  box-shadow: 0 4px 20px rgba(37, 99, 235, 0.15);
}

.dashboard-header-content {
  max-width: 1400px;
  margin: 0 auto;
  padding: 1.5rem 2rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.dashboard-brand {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.brand-logo {
  width: 3rem;
  height: 3rem;
  background: linear-gradient(135deg, #fbbf24 0%, #f59e0b 100%);
  color: #1e3a8a;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 900;
  font-size: 1.25rem;
  position: relative;
  box-shadow: 0 4px 15px rgba(251, 191, 36, 0.3);
}

.logo-pulse {
  position: absolute;
  top: -2px;
  left: -2px;
  right: -2px;
  bottom: -2px;
  border-radius: 50%;
  border: 2px solid rgba(251, 191, 36, 0.5);
  animation: pulse 2s ease-in-out infinite;
}

.dashboard-brand-title {
  font-size: 1.5rem;
  font-weight: 800;
  margin: 0;
}

.dashboard-brand-subtitle {
  font-size: 0.875rem;
  opacity: 0.9;
  margin: 0;
  font-weight: 500;
}

.dashboard-header-right {
  display: flex;
  align-items: center;
  gap: 2rem;
}

.time-widget {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  padding: 0.75rem 1.5rem;
  border-radius: 0.75rem;
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.time-icon {
  font-size: 1.25rem;
}

.time-info {
  display: flex;
  flex-direction: column;
}

.time-label {
  font-size: 0.75rem;
  opacity: 0.8;
  font-weight: 500;
}

.time-value {
  font-size: 0.875rem;
  font-weight: 600;
}

.search-widget {
  position: relative;
}

.search-widget .search-icon {
  position: absolute;
  left: 1rem;
  top: 50%;
  transform: translateY(-50%);
  height: 1rem;
  width: 1rem;
  color: #9ca3af;
}

.dashboard-search {
  padding: 0.75rem 1rem 0.75rem 2.5rem;
  border-radius: 0.75rem;
  border: 1px solid rgba(255, 255, 255, 0.2);
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  color: white;
  width: 250px;
  transition: all 0.3s ease;
}

.dashboard-search::placeholder {
  color: rgba(255, 255, 255, 0.7);
}

.dashboard-search:focus {
  outline: none;
  background: rgba(255, 255, 255, 0.15);
  border-color: #fbbf24;
  box-shadow: 0 0 0 3px rgba(251, 191, 36, 0.1);
}

.dashboard-nav {
  background: linear-gradient(135deg, #1d4ed8 0%, #1e40af 100%);
  padding: 0 2rem;
  display: flex;
  gap: 0.5rem;
  max-width: 1400px;
  margin: 0 auto;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1);
}

.nav-item {
  position: relative;
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 1rem 1.5rem;
  background: none;
  border: none;
  color: white;
  cursor: pointer;
  transition: all 0.3s ease;
  border-radius: 0.5rem 0.5rem 0 0;
  font-weight: 500;
  overflow: hidden;
}

.nav-item:hover {
  background: rgba(255, 255, 255, 0.1);
  transform: translateY(-2px);
}

.nav-item.active {
  background: #f8fafc;
  color: #1f2937;
  box-shadow: 0 -4px 20px rgba(37, 99, 235, 0.15);
}

.nav-indicator {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 3px;
  background: linear-gradient(135deg, #fbbf24 0%, #f59e0b 100%);
  transform: scaleX(0);
  transition: transform 0.3s ease;
}

.nav-item.active .nav-indicator {
  transform: scaleX(1);
}

.nav-icon {
  height: 1.125rem;
  width: 1.125rem;
}

.logout-btn {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 1rem 1.5rem;
  background: none;
  border: none;
  color: white;
  cursor: pointer;
  transition: all 0.3s ease;
  border-radius: 0.5rem;
  margin-left: auto;
  font-weight: 500;
}

.logout-btn:hover {
  background: rgba(220, 38, 38, 0.2);
  color: #fca5a5;
}

.dashboard-main {
  max-width: 1400px;
  margin: 0 auto;
  padding: 2.5rem 2rem;
}

.dashboard-content {
  background: white;
  border-radius: 1.5rem;
  padding: 2.5rem;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
  border: 1px solid rgba(226, 232, 240, 0.8);
}

.dashboard-title-section {
  margin-bottom: 3rem;
}

.title-wrapper {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.dashboard-title {
  display: flex;
  align-items: center;
  gap: 1rem;
  font-size: 2.5rem;
  font-weight: 900;
  color: #1f2937;
  margin: 0;
}

.title-icon {
  font-size: 2rem;
}

.dashboard-subtitle {
  color: #6b7280;
  font-size: 1.125rem;
  margin: 0;
}

.stats-cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1.5rem;
  margin-top: 2rem;
}

.stat-card {
  background: linear-gradient(135deg, #f8fafc 0%, #e2e8f0 100%);
  padding: 1.5rem;
  border-radius: 1rem;
  display: flex;
  align-items: center;
  gap: 1rem;
  border: 1px solid rgba(226, 232, 240, 0.8);
  transition: all 0.3s ease;
}

.stat-card:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 25px rgba(37, 99, 235, 0.1);
}

.stat-icon {
  font-size: 2rem;
  width: 3rem;
  height: 3rem;
  background: white;
  border-radius: 0.75rem;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.stat-info {
  display: flex;
  flex-direction: column;
}

.stat-number {
  font-size: 1.75rem;
  font-weight: 900;
  color: #1f2937;
}

.stat-label {
  font-size: 0.875rem;
  color: #6b7280;
  font-weight: 500;
}

.dashboard-controls {
  margin-bottom: 2.5rem;
}

.search-filter-container {
  display: flex;
  gap: 1.5rem;
  align-items: center;
}

.search-box {
  position: relative;
  flex: 1;
  max-width: 400px;
}

.search-box .search-icon {
  position: absolute;
  left: 1rem;
  top: 50%;
  transform: translateY(-50%);
  height: 1.125rem;
  width: 1.125rem;
  color: #9ca3af;
}

.search-input-dashboard {
  width: 100%;
  padding: 1rem 1rem 1rem 3rem;
  border: 1px solid #e5e7eb;
  border-radius: 0.75rem;
  font-size: 0.875rem;
  background: #f9fafb;
  transition: all 0.3s ease;
}

.search-input-dashboard:focus {
  outline: none;
  border-color: #2563eb;
  background: white;
  box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
}

.status-filter {
  padding: 1rem 1.5rem;
  border: 1px solid #e5e7eb;
  border-radius: 0.75rem;
  font-size: 0.875rem;
  background: #f9fafb;
  color: #374151;
  font-weight: 500;
  transition: all 0.3s ease;
}

.status-filter:focus {
  outline: none;
  border-color: #2563eb;
  background: white;
  box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
}

.cases-container {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  margin-bottom: 2.5rem;
}

.case-card {
  border: 1px solid #e5e7eb;
  border-radius: 1rem;
  padding: 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #f9fafb;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.case-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 4px;
  height: 100%;
  background: linear-gradient(135deg, #2563eb 0%, #1d4ed8 100%);
  transform: scaleY(0);
  transition: transform 0.3s ease;
}

.case-card:hover {
  background: white;
  box-shadow: 0 10px 25px rgba(37, 99, 235, 0.1);
  border-color: #2563eb;
}

.case-card:hover::before {
  transform: scaleY(1);
}

.case-info {
  flex: 1;
}

.case-header {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
  gap: 1.5rem;
}

.case-field {
  display: flex;
  flex-direction: column;
}

.case-label {
  font-size: 0.75rem;
  color: #6b7280;
  margin-bottom: 0.5rem;
  text-transform: uppercase;
  font-weight: 600;
  letter-spacing: 0.5px;
}

.case-id {
  font-size: 1.125rem;
  font-weight: 800;
  color: #2563eb;
  margin: 0;
}

.case-value {
  font-size: 1rem;
  color: #1f2937;
  margin: 0;
  font-weight: 600;
}

.case-actions {
  display: flex;
  align-items: center;
  gap: 1.5rem;
}

.status-badge {
  padding: 0.5rem 1rem;
  border-radius: 2rem;
  font-size: 0.75rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  border: 2px solid transparent;
}

.status-badge.resolved {
  background: linear-gradient(135deg, #dcfce7 0%, #bbf7d0 100%);
  color: #166534;
  border-color: #22c55e;
}

.status-badge.pending {
  background: linear-gradient(135deg, #fef3c7 0%, #fde68a 100%);
  color: #92400e;
  border-color: #f59e0b;
}

.status-badge.in-progress {
  background: linear-gradient(135deg, #dbeafe 0%, #bfdbfe 100%);
  color: #1e40af;
  border-color: #3b82f6;
}

.status-badge.ongoing {
  background: linear-gradient(135deg, #fed7aa 0%, #fdba74 100%);
  color: #c2410c;
  border-color: #f97316;
}

.view-more-btn {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0.75rem 1.5rem;
  background: linear-gradient(135deg, #2563eb 0%, #1d4ed8 100%);
  color: white;
  border: none;
  border-radius: 0.75rem;
  cursor: pointer;
  font-size: 0.875rem;
  font-weight: 600;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(37, 99, 235, 0.2);
}

.view-more-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(37, 99, 235, 0.3);
}

.view-icon {
  height: 1rem;
  width: 1rem;
}

.pagination {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: 2rem;
  border-top: 1px solid #e5e7eb;
}

.pagination-info {
  color: #6b7280;
  font-size: 0.875rem;
  font-weight: 500;
}

.pagination-controls {
  display: flex;
  gap: 0.75rem;
}

.pagination-btn {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 1rem;
  border: 1px solid #e5e7eb;
  background: white;
  color: #374151;
  border-radius: 0.5rem;
  cursor: pointer;
  font-size: 0.875rem;
  font-weight: 500;
  transition: all 0.3s ease;
}

.pagination-btn:hover:not(:disabled) {
  background: #f3f4f6;
  border-color: #2563eb;
  color: #2563eb;
}

.pagination-btn.active {
  background: linear-gradient(135deg, #2563eb 0%, #1d4ed8 100%);
  color: white;
  border-color: #2563eb;
  box-shadow: 0 4px 15px rgba(37, 99, 235, 0.2);
}

.pagination-btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.btn-icon {
  height: 1rem;
  width: 1rem;
}

/* Enhanced Form Styles */
.complaint-form {
  max-width: 1200px;
}

.form-sections {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2.5rem;
  margin-bottom: 3rem;
}

.form-section {
  background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%);
  padding: 2rem;
  border-radius: 1.5rem;
  border: 1px solid rgba(226, 232, 240, 0.8);
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
}

.section-header-form {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 2rem;
}

.section-icon {
  font-size: 1.5rem;
  width: 2.5rem;
  height: 2.5rem;
  background: white;
  border-radius: 0.75rem;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.section-title-form {
  font-size: 1.5rem;
  font-weight: 700;
  color: #1f2937;
  margin: 0;
}

.form-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.5rem;
}

.form-group {
  margin-bottom: 1.5rem;
}

.form-group label {
  display: block;
  margin-bottom: 0.75rem;
  font-weight: 600;
  color: #374151;
  font-size: 0.875rem;
}

.form-input, .form-select {
  width: 100%;
  padding: 1rem;
  border: 1px solid #e5e7eb;
  border-radius: 0.75rem;
  font-size: 0.875rem;
  background: white;
  transition: all 0.3s ease;
  font-weight: 500;
}

.form-input:focus, .form-select:focus {
  outline: none;
  border-color: #2563eb;
  box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
  background: #fefefe;
}

.form-input:disabled, .form-select:disabled {
  background: #f9fafb;
  color: #6b7280;
  cursor: not-allowed;
}

.form-textarea {
  width: 100%;
  padding: 1rem;
  border: 1px solid #e5e7eb;
  border-radius: 0.75rem;
  font-size: 0.875rem;
  resize: vertical;
  font-family: inherit;
  background: white;
  transition: all 0.3s ease;
  font-weight: 500;
  min-height: 120px;
}

.form-textarea:focus {
  outline: none;
  border-color: #2563eb;
  box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
}

.character-count {
  text-align: right;
  font-size: 0.75rem;
  color: #6b7280;
  margin-top: 0.5rem;
  font-weight: 500;
}

.character-count .text-warning {
  color: #f59e0b;
  font-weight: 600;
}

.form-note {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.75rem;
  color: #2563eb;
  margin-top: 1rem;
  padding: 0.75rem;
  background: rgba(37, 99, 235, 0.05);
  border-radius: 0.5rem;
  border: 1px solid rgba(37, 99, 235, 0.1);
}

.note-icon {
  font-size: 1rem;
}

.upload-section {
  margin-top: 2rem;
}

.upload-area {
  border: 2px dashed #d1d5db;
  border-radius: 1rem;
  padding: 3rem 2rem;
  text-align: center;
  background: white;
  transition: all 0.3s ease;
  cursor: pointer;
}

.upload-area:hover {
  border-color: #2563eb;
  background: #f8fafc;
}

.upload-icon {
  height: 3rem;
  width: 3rem;
  color: #9ca3af;
  margin: 0 auto 1rem;
}

.upload-area h4 {
  font-size: 1.125rem;
  font-weight: 600;
  color: #374151;
  margin-bottom: 0.5rem;
}

.upload-area p {
  color: #6b7280;
  margin-bottom: 1rem;
}

.upload-btn {
  background: linear-gradient(135deg, #2563eb 0%, #1d4ed8 100%);
  color: white;
  padding: 0.75rem 2rem;
  border: none;
  border-radius: 0.75rem;
  cursor: pointer;
  font-weight: 600;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(37, 99, 235, 0.2);
}

.upload-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(37, 99, 235, 0.3);
}

.upload-note {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  font-size: 0.75rem;
  color: #6b7280;
  margin-top: 1rem;
}

.form-actions {
  text-align: center;
  padding-top: 3rem;
  border-top: 1px solid #e5e7eb;
}

.proceed-btn {
  position: relative;
  background: linear-gradient(135deg, #10b981 0%, #059669 100%);
  color: white;
  padding: 1.25rem 3rem;
  border: none;
  border-radius: 1rem;
  font-size: 1.125rem;
  font-weight: 700;
  cursor: pointer;
  transition: all 0.3s ease;
  margin-bottom: 2rem;
  box-shadow: 0 10px 25px rgba(16, 185, 129, 0.3);
  overflow: hidden;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.proceed-btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 20px 40px rgba(16, 185, 129, 0.4);
}

.privacy-note {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.75rem;
  font-size: 0.75rem;
  color: #6b7280;
  max-width: 600px;
  margin: 0 auto;
  line-height: 1.5;
  padding: 1rem;
  background: #f9fafb;
  border-radius: 0.75rem;
  border: 1px solid #e5e7eb;
}

.privacy-icon {
  font-size: 1rem;
  color: #10b981;
}

.privacy-link {
  color: #2563eb;
  text-decoration: underline;
  font-weight: 600;
}

.privacy-link:hover {
  color: #1d4ed8;
}

/* Enhanced Calendar Styles */
.calendar-layout {
  display: grid;
  grid-template-columns: 2fr 1fr;
  gap: 2.5rem;
}

.calendar-main {
  background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%);
  border-radius: 1.5rem;
  padding: 2rem;
  border: 1px solid rgba(226, 232, 240, 0.8);
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
}

.calendar-header {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 2.5rem;
  gap: 3rem;
}

.calendar-nav-btn {
  background: white;
  border: 1px solid #e5e7eb;
  color: #2563eb;
  cursor: pointer;
  padding: 0.75rem;
  border-radius: 0.75rem;
  transition: all 0.3s ease;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
}

.calendar-nav-btn:hover {
  background: #2563eb;
  color: white;
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(37, 99, 235, 0.2);
}

.calendar-month {
  font-size: 2rem;
  font-weight: 900;
  color: #1f2937;
  margin: 0;
  text-align: center;
  min-width: 200px;
}

.calendar-grid {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  gap: 1px;
  background-color: #e5e7eb;
  border-radius: 1rem;
  overflow: hidden;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
}

.calendar-day-header {
  background: linear-gradient(135deg, #1f2937 0%, #374151 100%);
  color: white;
  padding: 1rem;
  text-align: center;
  font-weight: 700;
  font-size: 0.875rem;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.calendar-day {
  background-color: white;
  min-height: 100px;
  padding: 0.75rem;
  position: relative;
  cursor: pointer;
  transition: all 0.3s ease;
  border: 2px solid transparent;
}

.calendar-day:hover {
  background-color: #f8fafc;
  border-color: #2563eb;
}

.calendar-day.other-month {
  background-color: #f9fafb;
  color: #9ca3af;
}

.calendar-day.today {
  background: linear-gradient(135deg, #2563eb 0%, #1d4ed8 100%);
  color: white;
}

.calendar-day.today .day-number {
  font-weight: 900;
}

.calendar-day.has-event {
  background: linear-gradient(135deg, #fef3c7 0%, #fde68a 100%);
}

.day-number {
  font-size: 1rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
}

.day-events {
  margin-top: 0.5rem;
  display: flex;
  flex-direction: column;
  gap: 3px;
}

.event-bar {
  height: 6px;
  border-radius: 3px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.event-bar.resolved {
  background: linear-gradient(135deg, #10b981 0%, #059669 100%);
}

.event-bar.ongoing {
  background: linear-gradient(135deg, #f59e0b 0%, #d97706 100%);
}

.calendar-sidebar {
  background: white;
  border-radius: 1.5rem;
  padding: 2rem;
  height: fit-content;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
  border: 1px solid rgba(226, 232, 240, 0.8);
}

.sidebar-header {
  margin-bottom: 2rem;
}

.sidebar-title {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  font-size: 1.5rem;
  font-weight: 700;
  color: #1f2937;
  margin: 0;
}

.sidebar-icon {
  font-size: 1.25rem;
}

.hearings-list {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  margin-bottom: 2.5rem;
}

.hearing-card {
  background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%);
  border-radius: 1rem;
  padding: 1.5rem;
  border: 1px solid rgba(226, 232, 240, 0.8);
  transition: all 0.3s ease;
}

.hearing-card:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 25px rgba(37, 99, 235, 0.1);
  border-color: #2563eb;
}

.hearing-info {
  margin-bottom: 1.5rem;
}

.hearing-case {
  font-size: 1.125rem;
  font-weight: 800;
  color: #2563eb;
  margin-bottom: 0.75rem;
}

.hearing-type, .hearing-respondent {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.875rem;
  color: #6b7280;
  margin: 0.5rem 0;
  font-weight: 500;
}

.type-icon, .respondent-icon {
  font-size: 1rem;
}

.hearing-actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
}

.file-complaint-btn {
  width: 100%;
  background: linear-gradient(135deg, #2563eb 0%, #1d4ed8 100%);
  color: white;
  padding: 1rem;
  border: none;
  border-radius: 0.75rem;
  font-weight: 700;
  cursor: pointer;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.75rem;
  box-shadow: 0 4px 15px rgba(37, 99, 235, 0.2);
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.file-complaint-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(37, 99, 235, 0.3);
}

/* Enhanced Profile Styles */
.profile-layout {
  display: grid;
  grid-template-columns: 2fr 1fr;
  gap: 2.5rem;
}

.profile-main {
  background: linear-gradient(135deg, #f8fafc 0%, #f1f5f9 100%);
  border-radius: 1.5rem;
  padding: 2.5rem;
  border: 1px solid rgba(226, 232, 240, 0.8);
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
}

.profile-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 3rem;
}

.profile-title-section {
  flex: 1;
}

.profile-title {
  display: flex;
  align-items: center;
  gap: 1rem;
  font-size: 2rem;
  font-weight: 900;
  color: #1f2937;
  margin: 0 0 0.5rem 0;
}

.profile-subtitle {
  color: #6b7280;
  font-size: 1rem;
  margin: 0;
}

.edit-profile-btn {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  background: linear-gradient(135deg, #2563eb 0%, #1d4ed8 100%);
  color: white;
  padding: 0.75rem 1.5rem;
  border: none;
  border-radius: 0.75rem;
  cursor: pointer;
  font-size: 0.875rem;
  font-weight: 600;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(37, 99, 235, 0.2);
}

.edit-profile-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(37, 99, 235, 0.3);
}

.edit-icon {
  height: 1rem;
  width: 1rem;
}

.profile-form {
  margin-bottom: 2.5rem;
}

.profile-section {
  margin-bottom: 3rem;
}

.profile-section-title {
  font-size: 1.25rem;
  font-weight: 700;
  color: #1f2937;
  margin: 0;
}

.profile-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.5rem;
}

.profile-actions {
  text-align: center;
  padding-top: 2rem;
  border-top: 1px solid #e5e7eb;
}

.save-btn {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  background: linear-gradient(135deg, #10b981 0%, #059669 100%);
  color: white;
  padding: 1rem 2.5rem;
  border: none;
  border-radius: 0.75rem;
  font-weight: 700;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(16, 185, 129, 0.2);
  margin: 0 auto;
}

.save-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(16, 185, 129, 0.3);
}

.profile-status {
  background: white;
  border-radius: 1rem;
  padding: 1.5rem;
  border: 1px solid #d1fae5;
  box-shadow: 0 2px 8px rgba(16, 185, 129, 0.1);
}

.status-indicator {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  color: #065f46;
  font-weight: 600;
}

.status-icon {
  height: 1.5rem;
  width: 1.5rem;
  color: #10b981;
}

.profile-sidebar {
  background: white;
  border-radius: 1.5rem;
  padding: 2.5rem;
  height: fit-content;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
  border: 1px solid rgba(226, 232, 240, 0.8);
}

.profile-avatar {
  text-align: center;
  margin-bottom: 2.5rem;
}

.avatar-circle {
  position: relative;
  width: 6rem;
  height: 6rem;
  background: linear-gradient(135deg, #e5e7eb 0%, #d1d5db 100%);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 1.5rem;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
}

.avatar-icon {
  height: 3rem;
  width: 3rem;
  color: #6b7280;
}

.avatar-status {
  position: absolute;
  bottom: 4px;
  right: 4px;
  width: 1rem;
  height: 1rem;
  background: #10b981;
  border-radius: 50%;
  border: 2px solid white;
}

.profile-name {
  font-size: 1.5rem;
  font-weight: 800;
  color: #1f2937;
  margin: 0 0 0.5rem 0;
}

.profile-role {
  color: #6b7280;
  font-size: 0.875rem;
  font-weight: 500;
  margin: 0;
}

.profile-nav {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
  margin-bottom: 2.5rem;
}

.profile-nav-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 1rem 1.5rem;
  color: #6b7280;
  text-decoration: none;
  border-radius: 0.75rem;
  transition: all 0.3s ease;
  font-weight: 500;
  border: 1px solid transparent;
}

.profile-nav-item:hover {
  background: #f3f4f6;
  color: #1f2937;
  border-color: #e5e7eb;
}

.profile-nav-item.active {
  background: linear-gradient(135deg, #2563eb 0%, #1d4ed8 100%);
  color: white;
  box-shadow: 0 4px 15px rgba(37, 99, 235, 0.2);
}

.profile-nav-item .nav-icon {
  font-size: 1.125rem;
}

.nav-badge {
  background: #ef4444;
  color: white;
  font-size: 0.75rem;
  font-weight: 700;
  padding: 0.25rem 0.5rem;
  border-radius: 1rem;
  min-width: 1.25rem;
  text-align: center;
}

.profile-logout-btn {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  width: 100%;
  background: linear-gradient(135deg, #dc2626 0%, #b91c1c 100%);
  color: white;
  padding: 1rem 1.5rem;
  border: none;
  border-radius: 0.75rem;
  cursor: pointer;
  font-weight: 600;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(220, 38, 38, 0.2);
}

.profile-logout-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(220, 38, 38, 0.3);
}

.logout-icon {
  height: 1.125rem;
  width: 1.125rem;
}

/* Enhanced Modal Styles */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.6);
  backdrop-filter: blur(8px);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  animation: fadeIn 0.3s ease-out;
}

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

.modal-content {
  background: white;
  padding: 3rem;
  border-radius: 1.5rem;
  width: 90%;
  max-width: 450px;
  box-shadow: 0 25px 50px rgba(0, 0, 0, 0.25);
  border: 1px solid rgba(226, 232, 240, 0.8);
  animation: slideInUp 0.3s ease-out;
}

@keyframes slideInUp {
  from { opacity: 0; transform: translateY(30px); }
  to { opacity: 1; transform: translateY(0); }
}

.modal-header {
  text-align: center;
  margin-bottom: 2.5rem;
}

.modal-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
  display: block;
}

.modal-title {
  font-size: 1.75rem;
  font-weight: 800;
  margin-bottom: 0.5rem;
  color: #1f2937;
}

.modal-subtitle {
  color: #6b7280;
  font-size: 1rem;
  margin: 0;
}

.modal-actions {
  display: flex;
  gap: 1rem;
  margin-top: 2rem;
}

.cancel-btn {
  flex: 1;
  padding: 1rem;
  border: 1px solid #e5e7eb;
  background: white;
  color: #374151;
  border-radius: 0.75rem;
  cursor: pointer;
  font-weight: 600;
  transition: all 0.3s ease;
}

.cancel-btn:hover {
  background: #f3f4f6;
  border-color: #d1d5db;
}

.submit-btn {
  position: relative;
  flex: 1;
  padding: 1rem;
  background: linear-gradient(135deg, #2563eb 0%, #1d4ed8 100%);
  color: white;
  border: none;
  border-radius: 0.75rem;
  cursor: pointer;
  font-weight: 600;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(37, 99, 235, 0.2);
  overflow: hidden;
}

.submit-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(37, 99, 235, 0.3);
}

/* Responsive Design */
@media (max-width: 1024px) {
  .form-sections {
    grid-template-columns: 1fr;
  }
  
  .calendar-layout {
    grid-template-columns: 1fr;
  }
  
  .profile-layout {
    grid-template-columns: 1fr;
  }
  
  .profile-grid {
    grid-template-columns: 1fr;
  }
  
  .hero-title {
    font-size: 3rem;
  }
  
  .section-title {
    font-size: 2.5rem;
  }
  
  .mission-title {
    font-size: 2.5rem;
  }
  
  .footer-title {
    font-size: 2.5rem;
  }
}

@media (max-width: 768px) {
  .search-container {
    flex-direction: column;
    align-items: stretch;
  }
  
  .search-wrapper {
    flex-direction: column;
    gap: 0.5rem;
  }
  
  .search-btn {
    width: 100%;
  }
  
  .hero-title {
    font-size: 2.5rem;
  }
  
  .features-grid {
    grid-template-columns: 1fr;
  }
  
  .team-grid {
    grid-template-columns: 1fr;
  }
}

</style>