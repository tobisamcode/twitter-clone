<template>
  <div id="app" class="flex container h-screen w-full">
    <!-- side-bar -->
    <div class="lg:w-1/5 border-r border-lighter px-2 lg:px-6 py-2 flex flex-col items-center justify-between ">
      <div>
        <button class="h-12 w-12 hover:bg-lightblue text-3xl rounded-full text-blue">
          <i class="fab fa-twitter"></i>
        </button>
        <div>
          <button v-for="tab in tabs" :key="tab.id" @click="id = tab.id" :class="`focus:outline-none hover:text-blue flex items-center py-2 px-4 hover:bg-lightblue rounded-full mr-auto mb-3 ${ id === tab.id ? 'text-blue' : '' }`">
            <i :class="`${ tab.icon } text-2xl mr-4 text-left `"></i>
            <p class="hidden lg:block text-lg font-semibold text-left"> {{ tab.title }}  </p>
          </button>
        </div>
        <button class="text-white flex justify-center items-center bg-blue rounded-full font-semibold focus:outline-none w-12 h-12 lg:h-auto lg:w-full p-3 hover:bg-darkblue">
          <p class="hidden lg:block">Tweet</p>
          <i class="fas fa-plus text-sm lg:hidden"></i>
        </button>
      </div>
      <div class="lg:w-full relative">
        <button @click="showDropdown" class="flex items-center w-full hover:bg-lightblue rounded-full p-2">
          <img src="profile.jpg" class="w-10 h-10 rounded-full border border-lighter" />
          <div class="hidden lg:block ml-4">
            <p class="text-sm font-bold leading-tight">Tobi Samuel</p>
            <p class="text-sm leading-tight">@Tobisam100</p>
          </div>
          <i v-if="dropDown === false" class="hidden lg:block fas fa-angle-down ml-auto text-lg"></i>
          <i v-if="dropDown === true" class="hidden lg:block fas fa-angle-up ml-auto text-lg"></i>
        </button>
        <div v-if="dropDown === true" class="absolute bottom-0 left-0 w-64 rounded-lg shadow-md border-lightest bg-white mb-16">
          <button @click="dropDown = false" class="flex items-center w-full hover:bg-lightest p-3">
            <img src="profile.jpg" class="w-10 h-10 rounded-full border border-lighter" />
            <div class="ml-4">
              <p class="text-sm font-bold leading-tight">Tobi Samuel</p>
              <p class="text-sm leading-tight">@Tobisam100</p>
            </div>
            <i class="fas fa-check ml-auto text-blue"></i>
          </button>
          <button @click="dropDown = false" class="w-full text-left hover:bg-lightest border-t border-lighter p-3 text-sm">
            Add an existing account
          </button>
          <button @click="dropDown = false" class="w-full text-left hover:bg-lightest border-t border-lighter p-3 text-sm">
            Log out @Tobisam100
          </button>
        </div>
      </div>
    </div>
    <!-- tweet section -->
    <div class="w-1/2 h-full">

    </div>
    <!-- trending-section -->
    <div class="hidden md:block w-1/3 h-full border-l border-lighter py-2 px-6 overflow-y-scroll relative">
      <input class="pl-12  rounded-full w-full p-2 bg-lighter text-sm" placeholder="Search Twitter"/>
      <i class="fas fa-search absolute left-12 top-0  mt-4 text-sm text-light"></i>
      <div class="w-full rounded-lg bg-lightest my-4">
        <div class="flex items-center justify-between p-3">
          <p class="text-lg font-bold">Trends for You</p>
          <i class="fas fa-cog text-blue"></i>
        </div>
        <button v-for="trend in trending" :key="trend.top" class="w-full flex justify-between hover:bg-lighter p-3 border-t border-lighter">
          <div>
            <p class="text-sm text-left leading-tight text-dark"> {{trend.top}} </p>
            <p class="text-bold text-left leading-tight"> {{trend.title}} </p>
            <p class="text-left leading-tight text-dark"> {{trend.button}} </p>
          </div>
          <i class="fas fa-angle-down text-lg text-dark"></i>
        </button>
        <button class="w-full hover:bg-lighter p-3 border-t border-lighter text-blue text-left">Show More</button>
      </div>

      <div class="w-full rounded-lg bg-lightest my-6">
        <div class="p-3">
          <p class="text-lg font-bold">Who to Follow</p>
          <i class="fas fa-cog text-blue"></i>
        </div>
        <button v-for="friend in friends" :key="friend.name" class="w-full flex hover:bg-lighter p-3 border-t border-lighter">
          <img :src="`${friend.src}`" class="w-12 h-12 rounded-full border border-lighter" />
          <div class="hidden lg:block ml-4">
            <p class="text-sm font-bold leading-tight"> {{friend.name}} </p>
            <p class="text-sm leading-tight"> {{friend.handle}} </p>
          </div>
          <button class="text-sm tetx-blue py-1 ml-auto px-4 rounded-full border-2 border-blue ">Follow</button>
        </button>
        <button class="w-full hover:bg-lighter p-3 border-t border-lighter text-blue text-left">Show More</button>
      </div>
    </div>
  </div>
</template>

<script>  
export default {
  name: 'app',
  components: {},
  data() {
    return{
      tabs: [
        {icon: 'fas fa-home', title: 'Home', id:'home'},
        {icon: 'fas fa-hashtag', title: 'Explore', id: 'explore'},
        {icon: 'far fa-bell', title: 'Notifications', id: 'notifications'},
        {icon: 'far fa-envelope', title: 'Messages', id: 'messages'},
        {icon: 'far fa-bookmark', title: 'Bookmarks', id: 'bookmarks'},
        {icon: 'fas fa-clipboard-list', title: 'Lists', id: 'lists'},
        {icon: 'far fa-user', title: 'Profile', id: 'profile'},
        {icon: 'fas fa-ellipsis-h', title: 'More', id: 'more'}
      ],
      id: 'home',
      dropDown: false,
      trending: [
        {top: 'Trending in TX', title: 'Gigi', bottom: 'Trending with: Rip Gigi'},
        {top: 'Music', title: 'We Won', bottom: '135K Tweets'},
        {top: 'Pop', title: 'Blue Ivy', bottom: '40k tweets'},
        {top: 'Trending in US', title: 'Denim Day', bottom: '40k tweets'},
        {top: 'Trending', title: 'When Beyonce', bottom: '25.4k tweets'},
      ],
      friends: [
        {src: 'img1.jpg', name: 'Elon Musk', handle: '@teslaBoy'},
        {src: 'img2.jpg', name: 'Adrian Monk', handle: '@detective:)'},
        {src: 'img3.jpg', name: 'Kevin Hart', handle: '@miniRock'}
      ],
    }
  },
  methods: {
    showDropdown(){
      this.dropDown = !this.dropDown;
    }
  }
}
</script>