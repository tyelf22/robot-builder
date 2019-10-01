<template>
      <v-container>
        <div class="content">
          <v-btn class="addToCart"><v-icon>mdi-shopping</v-icon> Add to Cart</v-btn>
        </div>
        <div class="robot-name">
          {{selectedRobot.head.title}}
          <span v-if="selectedRobot.head.onSale" class="sale">Sale!</span>
        </div>
    <div class="top-row">
      <div class="top part">
        <img :src="selectedRobot.head.src" title="head"/>
        <v-btn fab small dark color="primary" @click="selectPreviousHead()" class="prev-up-top">
          <v-icon>mdi-arrow-left</v-icon>
        </v-btn>
        <v-btn fab small dark color="primary" @click="selectNextHead()" class="next-up-top">
          <v-icon>mdi-arrow-right</v-icon>
        </v-btn>
      </div>
    </div>
    <div class="middle-row">
      <div class="left part">
        <img :src="selectedRobot.leftArm.src" title="left arm"/>
        <v-btn fab small dark color="primary" @click="selectPreviousLeftArm" class="prev-selector">
          <v-icon>mdi-arrow-up</v-icon>
        </v-btn>
        <v-btn  fab small dark color="primary" @click="selectNextLeftArm" class="next-selector">
          <v-icon>mdi-arrow-down</v-icon>
        </v-btn>
      </div>
      <div class="center part">
        <img :src="selectedRobot.torso.src" title="torso"/>
        <v-btn fab small dark color="primary" @click="selectPrevTorso" class="prev-selector">
          <v-icon>mdi-arrow-left</v-icon>
        </v-btn>
        <v-btn fab small dark color="primary" @click="selectNextTorso" class="next-selector">
          <v-icon>mdi-arrow-right</v-icon>
        </v-btn>
      </div>
      <div class="right part">
        <img :src="selectedRobot.rightArm.src" title="right arm"/>
        <v-btn fab small dark color="primary" @click="selectPrevRightArm" class="prev-selector-right">
          <v-icon>mdi-arrow-up</v-icon>
        </v-btn>
        <v-btn fab small dark color="primary" @click="selectNextRightArm" class="next-selector-right">
          <v-icon>mdi-arrow-down</v-icon>
        </v-btn>
      </div>
    </div>
    <div class="bottom-row">
      <div class="bottom part">
        <img :src="selectedRobot.base.src" title="bottom"/>
        <v-btn fab small dark color="primary" @click="selectPrevBottom" class="prev-selector-base">
          <v-icon>mdi-arrow-left</v-icon>
        </v-btn>
        <v-btn fab small dark color="primary"  @click="selectNextBottom" class="next-selector-base">
          <v-icon>mdi-arrow-right</v-icon>
        </v-btn>
      </div>
    </div>
    <div class="bottom-btn">
        <v-btn @click="randomRobot" rounded x-large max-width="5px;" color='primary'>Random</v-btn>
    </div>
  </v-container>
</template>

<script>
import availableParts from '../data/parts';
import {VBtn, VIcon} from 'vuetify/lib'


function getPreviousValidIndex(index, length) {
    const deprecatedIndex = index - 1;
    return deprecatedIndex < 0 ? length - 1 : deprecatedIndex;
}

function getNextValidIndex(index, length) {
    const incrementedIndex = index + 1;
    return incrementedIndex > length - 1 ? 0 : incrementedIndex;
}

function getRandomInt(max) {
  return Math.floor(Math.random() * Math.floor(max));
}

export default {
    name: 'RobotBuilder',
    data() {
        return {
            availableParts,
            selectNextHeadIndex: 0,
            selectNextLeftArmIndex: 0,
            selectNextRightArmIndex: 0, 
            selectNextTorsoIndex: 0,
            selectNextBottomIndex: 0,
        };
    },
    components: function () {
        return {
            VBtn,
            VIcon
        };
    },

    computed: {
      selectedRobot() {
        return {
          head: availableParts.heads[this.selectNextHeadIndex],
          leftArm: availableParts.arms[this.selectNextLeftArmIndex],
          rightArm: availableParts.arms[this.selectNextRightArmIndex],
          torso: availableParts.torsos[this.selectNextTorsoIndex],
          base: availableParts.bases[this.selectNextBottomIndex],
        };
      },

    },
    methods: {
        selectNextHead() {
            this.selectNextHeadIndex = getNextValidIndex(this.selectNextHeadIndex, availableParts.heads.length);
           
        },
        selectPreviousHead() {
            this.selectNextHeadIndex = getPreviousValidIndex(this.selectNextHeadIndex, availableParts.heads.length);
           
        },
        selectNextLeftArm() {
            this.selectNextLeftArmIndex = getNextValidIndex(this.selectNextLeftArmIndex, availableParts.arms.length);
        },
        selectPreviousLeftArm() {
            this.selectNextLeftArmIndex = getPreviousValidIndex(this.selectNextLeftArmIndex, availableParts.arms.length);

        },
        selectPrevRightArm() {
            this.selectNextRightArmIndex = getPreviousValidIndex(this.selectNextRightArmIndex, availableParts.arms.length);
        },
        selectNextRightArm() {
            this.selectNextRightArmIndex = getNextValidIndex(this.selectNextRightArmIndex, availableParts.arms.length);
        },
        selectNextTorso() {
            this.selectNextTorsoIndex = getNextValidIndex(this.selectNextTorsoIndex, availableParts.torsos.length);
        },
        selectPrevTorso() {
            this.selectNextTorsoIndex = getPreviousValidIndex(this.selectNextTorsoIndex, availableParts.torsos.length);
        },
        selectNextBottom() {
            this.selectNextBottomIndex = getNextValidIndex(this.selectNextBottomIndex, availableParts.bases.length);
        },
        selectPrevBottom() {
            this.selectNextBottomIndex = getPreviousValidIndex(this.selectNextBottomIndex, availableParts.bases.length);
        },
        randomRobot() {
          this.selectNextHeadIndex = getRandomInt(5);
          this.selectNextLeftArmIndex = getRandomInt(5);
          this.selectNextRightArmIndex = getRandomInt(5);
          this.selectNextTorsoIndex = getRandomInt(3);
          this.selectNextBottomIndex = getRandomInt(5);
        }

    }
}
</script>

<style scoped>

.part {
  position: relative;
  width:165px;
  height:165px;
} 
.part img {
  width:165px;
}
.top-row {
  display:flex;
  justify-content: space-around;
}
.middle-row {
  display:flex;
  justify-content: center;
}
.bottom-row {
  display:flex;
  justify-content: space-around;
  border-top: none;
}

.bottom-btn {
  display: flex;
  justify-content: center;
  margin-top: 80px;
}

.head {
  border-bottom: none;
}
.left {
  border-right: none;
}
.right {
  border-left: none;
}
.left img {
  transform: rotate(-90deg);
}
.right img {
  transform: rotate(90deg);
}
.bottom {
  border-top: none;
}
.prev-selector {
  position: absolute;
  z-index:1;
  top: 130px;
  left: -45px;
}

.prev-selector-base {
  position: absolute;
  z-index:1;
  top: 170px;
  left: 30px;
}

.next-selector-base {
  position: absolute;
  z-index:1;
  top: 170px;
  right: 30px;

}


.prev-up-top {
  position: absolute;
  z-index:1;
  top: -50px;
  left: 30px;
}


.next-up-top {
    position: absolute;
  z-index:1;
  top: -50px;
  right: 30px;
}

.next-selector {
  position: absolute;
  z-index:1;
  top: 130px;
  right: -45px;
}

.left .prev-selector {
  top: 30px;
  left: -45px;
}
.left .next-selector {
  top: auto;
  bottom: 30px;
  left: -45px;    
}
.right .prev-selector-right {
  top: -140px;
  left: 170px;  
}
.right .next-selector-right {
  bottom: 75px;
  left: 130px;    
}
.right .next-selector {
  right: -3px;
}

.robot-name {
  position: absolute;
  top: 5px;
  left: 2px;
  text-align: center;
  width: 100%;
  font-size: 23px;
  font-family: 'Audiowide', sans-serif;
  }

  .sale {
    color: red;
  }

  .content {
    position: relative;
  }

  .addToCart {
    position: absolute;
    right: 30px;
    top: -100px;
  }

</style>