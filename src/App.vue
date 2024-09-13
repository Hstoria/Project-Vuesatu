<template>
  <div class="dashboard">
    <header>
      <h1 class="title">
        <span class="animated-text">
          <span
            v-for="(letter, index) in 'Hola Amigos!'"
            :key="index"
            class="letter"
            :style="{ animationDelay: `${index * 0.1}s` }"
          >
            {{ letter === ' ' ? '\u00A0' : letter }}
          </span>
        </span>
      </h1>
    </header>

    <main>
      <section class="card counter">
        <h2>Counter</h2>
        <div class="content">
          <p class="count" :class="{ 'count-changed': countChanged }">{{ count }}</p>
          <div>
            <button @click="incrementCount" class="btn">+</button>
            <button @click="resetCount" class="btn secondary">Reset</button>
          </div>
        </div>
      </section>

      <section class="card color-changer">
        <h2>Color Changer</h2>
        <div class="content">
          <div class="color-box" :style="{ backgroundColor: boxColor }"></div>
          <button @click="changeColor" class="btn">Change Color</button>
        </div>
      </section>

      <section class="card carousel">
        <h2>Image Carousel</h2>
        <div class="content">
          <div class="image-container">
            <transition-group name="fade">
              <img
                v-for="(image, index) in images"
                :key="image"
                :src="image"
                v-show="index === currentImageIndex"
                alt="Carousel Image"
                class="carousel-image"
              />
            </transition-group>
          </div>
          <div class="carousel-controls">
            <button @click="prevImage" class="btn">&larr;</button>
            <button @click="nextImage" class="btn">&rarr;</button>
          </div>
        </div>
      </section>
    </main>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      count: 0,
      countChanged: false,
      boxColor: '#6D28D9',
      images: [
        'https://i.pinimg.com/originals/3b/af/18/3baf18514a40de4ef021061000b7e80f.jpg',
        'https://i.pinimg.com/originals/fa/39/94/fa3994683ed6aba50dcb5a7cbb89f9fa.jpg',
        'https://i.pinimg.com/originals/4d/40/51/4d40511945090cd87a81885411fdeb97.jpg',
        'https://i.pinimg.com/originals/ef/e2/f5/efe2f5ff7b8b9a05d5b9c34ddab11044.jpg',
        'https://i.pinimg.com/originals/16/48/21/164821329daeeb48225d634e4f4bbaf5.jpg'
      ],
      currentImageIndex: 0
    }
  },
  methods: {
    incrementCount() {
      this.count++
      this.animateCount()
    },
    resetCount() {
      this.count = 0
      this.animateCount()
    },
    animateCount() {
      this.countChanged = true
      setTimeout(() => {
        this.countChanged = false
      }, 300)
    },
    changeColor() {
      const colors = ['#6D28D9', '#059669', '#DC2626', '#2563EB', '#D97706']
      this.boxColor = colors[Math.floor(Math.random() * colors.length)]
    },
    nextImage() {
      this.currentImageIndex = (this.currentImageIndex + 1) % this.images.length
    },
    prevImage() {
      this.currentImageIndex =
        (this.currentImageIndex - 1 + this.images.length) % this.images.length
    }
  }
}
</script>

<style>
.dashboard {
  font-family: Arial, sans-serif;
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

.title {
  text-align: center;
  color: #6d28d9;
  font-size: 2.5rem;
  margin-bottom: 2rem;
}

.card {
  background-color: white;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  padding: 20px;
  margin-bottom: 20px;
  transition: transform 0.3s ease;
}

.card:hover {
  transform: translateY(-5px);
}

h2 {
  color: #4b5563;
  margin-top: 0;
}

.content {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.count {
  font-size: 3rem;
  font-weight: bold;
  color: #6d28d9;
  transition: transform 0.3s ease;
}

.count-changed {
  transform: scale(1.2);
}

.color-box {
  width: 100px;
  height: 100px;
  border-radius: 8px;
  margin: 10px 0;
  transition: transform 2s linear;
  animation: rotate 4s linear infinite;
}

@keyframes rotate {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

.btn {
  background-color: #6d28d9;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 20px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  margin: 5px;
}

.btn:hover {
  background-color: #5b21b6;
}

.btn.secondary {
  background-color: #9ca3af;
}

.btn.secondary:hover {
  background-color: #6b7280;
}

.image-container {
  position: relative;
  width: 100%;
  height: 300px;
  overflow: hidden;
  border-radius: 8px;
}

.carousel-image {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.carousel-controls {
  display: flex;
  justify-content: space-between;
  margin-top: 10px;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.animated-text {
  display: inline-block;
}

.letter {
  display: inline-block;
  opacity: 0;
  animation: fadeIn 0.5s forwards;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
