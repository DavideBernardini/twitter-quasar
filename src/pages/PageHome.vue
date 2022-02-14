<template>
  <q-page class="relative-position">
    <q-scroll-area class="absolute fullscreen">
      <div class="row q-py-lg q-px-md items-end q-col-gutter-md">
        <div class="col">
          <q-input
            class="new-qweet"
            bottom-slots
            v-model="newQweetContent"
            placeholder="What's happening?"
            counter
            maxlength="280"
            autogrow
          >
            <template v-slot:before>
              <q-avatar size="xl">
                <img src="../assets/Davide-Bernardini-CV.png" />
              </q-avatar>
            </template>
          </q-input>
        </div>
        <div class="col col-shrink">
          <q-btn
            class="q-mb-lg"
            unelevated
            rounded
            color="primary"
            label="Qweet"
            no-caps
            :disable="!newQweetContent"
            @click="addNewQweet()"
          />
        </div>
      </div>
      <q-separator class="divider" size="10px" color="grey-2" />
      <q-list separator>
        <transition-group
          appear
          enter-active-class="animated fadeIn"
          leave-active-class="animated fadeOut"
        >
          <q-item class="q-py-md" v-for="qweet in qweets" :key="qweet.date">
            <q-item-section avatar top>
              <q-avatar size="xl">
                <img src="../assets/Davide-Bernardini-CV.png" />
              </q-avatar>
            </q-item-section>

            <q-item-section>
              <q-item-label class="text-subtitle1"
                ><strong>Davide Bernardini</strong>
                <span class="text-grey-7 q-mr-sm"> @Davide_Brn </span>
                <br class="lt-md" />
                <span class="text-grey-7"> {{ timeSince(qweet.date) }}</span>
              </q-item-label>
              <q-item-label class="qweet-content text-body1">
                {{ qweet.content }}
              </q-item-label>
              <div class="qweet-icons row justify-between q-mt-sm">
                <q-btn
                  flat
                  round
                  color="grey"
                  icon="far fa-comment"
                  size="sm"
                />
                <q-btn
                  flat
                  round
                  color="grey"
                  icon="fas fa-retweet"
                  size="sm"
                />
                <q-btn
                  flat
                  round
                  :color="qweet.liked ? 'pink' : 'gray'"
                  :icon="qweet.liked ? 'fas fa-heart' : 'far fa-heart'"
                  size="sm"
                  @click="qweet.liked = !qweet.liked"
                />
                <q-btn
                  flat
                  round
                  color="grey"
                  icon="fas fa-trash"
                  size="sm"
                  @click="deleteQweet(qweet)"
                />
              </div>
            </q-item-section>
          </q-item>
        </transition-group>
      </q-list>
    </q-scroll-area>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "PageHome",
  data() {
    return {
      newQweetContent: "",
      qweets: [
        {
          content:
            "Lorem ipsum dolor sit amet, consectetur adipisicing elit. Cumque voluptate repellendus molestiae.",
          date: new Date(2022, 1, 14, 11, 10, 0),
          liked: false,
        },
        {
          content:
            "\“People who can’t throw something important away, can never hope to change anything.\” \n \n--Armin Arlelt",
          date: new Date(2022, 1, 13, 23, 10, 0),
          liked: true,
        },
        {
          content:
            "Lorem ipsum dolor sit, illo voluptatum unde, vel odit quasi reiciendis omnis nam sequi!",
          date: new Date(2022, 1, 12, 17, 10, 0),
          liked: false,
        },
        {
          content:
            "\“We keep moving forward, opening new doors, and doing new things, because we're curious and curiosity keeps leading us down new paths.\” \n \n--Walt Disney",
          date: new Date(2022, 1, 11, 16, 10, 0),
          liked: false,
        },
      ],
    };
  },
  methods: {
    timeSince(timeStamp) {
      let now = new Date();
      let secondsPast = (now.getTime() - timeStamp) / 1000;
      if (secondsPast < 60) {
        return "less than a minute";
      }
      if (secondsPast >= 60 && secondsPast < 120) {
        return "1 minute";
      }
      if (secondsPast < 3600) {
        return parseInt(secondsPast / 60) + " minutes";
      }
      if (secondsPast <= 86400) {
        return parseInt(secondsPast / 3600) + " hours";
      }
      if (secondsPast > 86400) {
        let day = timeStamp.getDate();
        let month = timeStamp
          .toDateString()
          .match(/ [a-zA-Z]*/)[0]
          .replace(" ", "");
        let year =
          timeStamp.getFullYear() == now.getFullYear()
            ? ""
            : " " + timeStamp.getFullYear();
        return day + " " + month + year;
      }
    },
    addNewQweet() {
      let newQweet = {
        content: this.newQweetContent,
        date: new Date().getTime(),
      };
      this.qweets.unshift(newQweet);
      this.newQweetContent = "";
    },
    deleteQweet(qweet) {
      let dateToDelete = qweet.date;
      let index = this.qweets.findIndex((qweet) => qweet.date === dateToDelete);
      this.qweets.splice(index, 1);
    },
  },
});
</script>

<style lang="scss">
.new-qweet {
  font-size: 19px;
  textarea {
    line-height: 1.4 !important;
  }
}
.divider {
  border-top: 1px solid;
  border-bottom: 1px solid;
  border-color: $grey-4;
}
.qweet-content {
  white-space: pre-line;
}
.qweet-icons {
  margin-left: -5px;
}
.fullscreen {
  z-index: 0;
}
</style>
