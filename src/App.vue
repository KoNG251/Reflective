<template>
  <div class="flex items-center justify-center flex-col h-screen p-3 sm:p-0">
    <div
      class="w-full h-full max-w-[35rem] max-h-[25rem] bg-white rounded-xl shadow-lg p-6 sm:p-8 relative"
    >
      <h1 class="text-2xl font-bold text-center mb-4 text-black">My Diary</h1>
      <textarea
        v-model="story"
        class="w-full h-32 bg-white resize-none p-2 border border-gray-300 rounded text-black"
        placeholder="บอกเรื่องราวที่คุณเจอวันนี้"
      ></textarea>
      <button
        class="btn rounded-full w-20 sm:w-40 absolute right-2 bottom-2 text-white py-2"
        @click="handleStory"
      >
        SAVE
      </button>
    </div>

    <div class="w-full flex overflow-x-scroll mx-5 mt-8">
      <div
        class="p-4 w-auto min-w-[14rem] max-w-[20rem] break-words h-auto bg-white shadow-xl text-black rounded-md mx-3"
        v-for="item in diary"
        :key="item"
      >
        <h4>วันที่ {{ formatThaiDate(item.date) }}</h4>
        <h5 class="mt-2">เนื้อหา</h5>
        <p>{{ item.content }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      titlename: 'Reflective Pages',
      story: '',
      diary: [],
      nextId: 1
    }
  },
  methods: {
    handleStory() {
      if (this.story.trim()) {
        const newStory = {
          id: this.nextId++,
          content: this.story,
          date: new Date()
        }
        this.diary.push(newStory)
        this.story = ''
      }
    },
    formatThaiDate(date) {
      const result = date.toLocaleDateString('th-TH', {
        year: 'numeric',
        month: 'long',
        day: 'numeric'
      })

      return result
    }
  },
  mounted() {
    document.title = this.titlename
  }
}
</script>
