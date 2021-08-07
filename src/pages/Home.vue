<template>
  <div class="datepicker">
    <input type="datetime-local" id="date" name="date picker" v-model="dateSelected" />
  </div>

  <div class="cards">
    <div v-for="(format, type, index) in times" :key="index" class="card">
      <span class="timestamp">{{ formatDate(dateSelected, format) }}</span>
      <code @click="copyToClipboard(formatDateCode(type), $event)">
        <pre><span>{{ formatDateCode(type) }}</span></pre>
      </code>
    </div>
  </div>
  <Toast />
</template>

<script>
import { ref, computed } from "vue";
import Toast from "../components/Toast.vue";
import moment from "moment";

export default {
  components: { Toast },
  setup() {
    const dateSelected = ref(moment().format("YYYY-MM-DDThh:mm"));
    const dateTimestamp = computed(() => {
      return moment(dateSelected.value) / 1000;
    });
    const formatDateCode = (type) =>
      `<t:${Math.round(moment(dateSelected.value) / 1000)}:${type}>`;
    const copyToClipboard = function (code, event) {
      var pre = event.target;
      var className = "shake-vertical";

      navigator.clipboard.writeText(code);
      pre.classList.toggle(className);
      setTimeout(() => pre.classList.remove(className), 2000);
      showToast()
    };

    const showToast = function () {
      var x = document.getElementById("snackbar");
      x.className = "show";
      setTimeout(function () {
        x.className = x.className.replace("show", "");
      }, 5000);
    };

    // get the user's local, en for US and en-GB for UK.
    // This is important, because the UK date is correct way round.
    var locale = window.navigator.userLanguage || window.navigator.language;

    const times = {
      t: "hh:mm",
      T: "HH:mm:ss",
      d: "L",
      D: "LL",
      f: "LLL",
      F: "LLLL",
      R: "R",
    };

    const formatDate = function (string, type) {
      if (type == "R") {
        return moment(string).fromNow();
      }
      return moment(string).locale(locale).format(type);
    };

    return {
      dateSelected,
      formatDate,
      dateTimestamp,
      times,
      locale,
      copyToClipboard,
      formatDateCode,
    };
  },
};
</script>

<style scoped>
input {
  padding: 8px;
  background: #2f3136;
  color: #dcddde;
  border: solid 1px #202225;
  border-radius: 4px;
  font-family: inherit;
  font-size: 1.2rem;
  width: 100%;
  max-width: 400px;
}
code:hover {
  cursor: pointer;
}
pre:hover:before{
  content: "Copy to clipboard";
}
pre:hover span{
  display: none;
}

.datepicker {
  display: flex;
  justify-content: center;
  padding: 2rem;
}
.shake-vertical {
  -webkit-animation: shake-vertical 0.8s cubic-bezier(0.455, 0.03, 0.515, 0.955) both;
  animation: shake-vertical 0.8s cubic-bezier(0.455, 0.03, 0.515, 0.955) both;
}

@-webkit-keyframes shake-vertical {
  0%,
  100% {
    -webkit-transform: translateY(0);
    transform: translateY(0);
  }
  10%,
  30%,
  50%,
  70% {
    -webkit-transform: translateY(-8px);
    transform: translateY(-8px);
  }
  20%,
  40%,
  60% {
    -webkit-transform: translateY(8px);
    transform: translateY(8px);
  }
  80% {
    -webkit-transform: translateY(6.4px);
    transform: translateY(6.4px);
  }
  90% {
    -webkit-transform: translateY(-6.4px);
    transform: translateY(-6.4px);
  }
}
@keyframes shake-vertical {
  0%,
  100% {
    -webkit-transform: translateY(0);
    transform: translateY(0);
  }
  10%,
  30%,
  50%,
  70% {
    -webkit-transform: translateY(-8px);
    transform: translateY(-8px);
  }
  20%,
  40%,
  60% {
    -webkit-transform: translateY(8px);
    transform: translateY(8px);
  }
  80% {
    -webkit-transform: translateY(6.4px);
    transform: translateY(6.4px);
  }
  90% {
    -webkit-transform: translateY(-6.4px);
    transform: translateY(-6.4px);
  }
}
.cards {
  display: grid;
  justify-content: center;
  grid-template-columns: repeat(2, 1fr);
  grid-gap: 1rem;
}
.card {
  border: solid 1px #202225;
  padding: 1rem;
  background: #2f3136;
}

input::-webkit-calendar-picker-indicator {
  background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="16" height="15" viewBox="0 0 24 24"><path fill="%23bbbbbb" d="M20 3h-1V1h-2v2H7V1H5v2H4c-1.1 0-2 .9-2 2v16c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zm0 18H4V8h16v13z"/></svg>');
}

.timestamp {
  background: hsla(0, 0%, 100%, 0.06);
  border-radius: 3px;
  padding: 0 2px;
}
</style>
