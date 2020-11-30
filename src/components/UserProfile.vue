<template>
<div class="user-profile">
    <div class="user-profile__user-panel">
        <h1 class="user-profile__username">@{{ state.user.username }}</h1>
        <div class="user-profile__admin-badge"  v-if="state.user.isAdmin">
          admin
        </div>
        
        <div class="user-profile__follower-count">
            <strong>Followers: </strong> {{ state.followers }}
        </div>
        <create-twoot-panel @add-twoot="addTwoot"></create-twoot-panel>
        
    </div>
    <div class="user-profile__twoots-wrapper">
      <TwootItem v-for="twoot in state.user.twoots" :key="twoot.id" :username="state.user.username" :twoot="twoot" @favourite="toggleFavourite"/>
        
    </div>
    </div>
</template>

<script>
import { reactive } from 'vue';
import TwootItem from "./TwootItem";
import CreateTwootPanel from "./CreateTwootPanel"
 
export default {
  components: {
    TwootItem, CreateTwootPanel },
    setup() {
      const state = reactive ({
         followers: 0,
      user: {
        id: 1,
        username: 'troymendous',
        firstName: 'Troy',
        lastName: 'Wilson',
        email: 'troy.wilson.was.taken@gmail.com',
        isAdmin: true,
        twoots:  [
          { id: 1, content: 'Twotter is amazing!'},
          { id: 2, content: "Don't forget to like and subscribe"}
        ]
      
      }

      })
    

  function addTwoot(twoot) {
    state.user.twoots.unshift({ id: state.user.twoots.length + 1, content: twoot});
  }
 
    return {
      state,
      addTwoot
  }
    }
};
</script>

<style lang="scss" scoped>
.user-profile {
    display: grid;
    grid-template-columns: 1fr 3fr;
    width: 100%;
    padding: 50px 5%;

    &__user-panel {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #DFE3E8;

    h1 {
    margin: 0;
}


  .user-profile__admin-badge {
  background: rebeccapurple;
  color: white;
  border-radius: 5px;
  margin-right: auto;
  padding: 0 10px;
  font-weight: bold;
  margin-bottom: 20px;
}

.user-profile__create-twoot {
  padding-top: 24px;
  border-top: 1px solid #DFE3E8;
  display: flex;
  flex-direction: column;

 
}

}

.user-profile__twoots-wrapper {
  display: grid;
  grid-gap: 16px;
  margin-bottom: auto;
}


}


</style>