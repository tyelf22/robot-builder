<template>
      <v-container>
    <div class="top-row">
      <div class="top part">
        <img v-bind:src="availableParts.heads[ selectNextHeadIndex ].src" title="head"/>
        <v-btn fab small dark color="primary" @click="selectPreviousHead()" class="prev-up">
          <v-icon>mdi-arrow-left</v-icon>
        </v-btn>
        <v-btn fab small dark color="primary" @click="selectNextHead()" class="next-up">
          <v-icon>mdi-arrow-right</v-icon>
        </v-btn>
      </div>
    </div>
    <div class="middle-row">
      <div class="left part">
        <img v-bind:src="availableParts.arms[ selectNextLeftArmIndex ].src" title="left arm"/>
        <v-btn fab small dark color="primary" @click="selectPreviousLeftArm" class="prev-selector">
          <v-icon>mdi-arrow-up</v-icon>
        </v-btn>
        <v-btn  fab small dark color="primary" @click="selectNextLeftArm" class="next-selector">
          <v-icon>mdi-arrow-down</v-icon>
        </v-btn>
      </div>
      <div class="center part">
        <img v-bind:src="availableParts.torsos[selectNextTorsoIndex].src" title="torso"/>
        <v-btn fab small dark color="primary" @click="selectPrevTorso" class="prev-selector">
          <v-icon>mdi-arrow-left</v-icon>
        </v-btn>
        <v-btn fab small dark color="primary" @click="selectNextTorso" class="next-selector">
          <v-icon>mdi-arrow-right</v-icon>
        </v-btn>
      </div>
      <div class="right part">
        <img v-bind:src="availableParts.arms[ selectNextRightArmIndex ].src" title="right arm"/>
        <v-btn fab small dark color="primary" @click="selectPrevRightArm" class="prev-selector">
          <v-icon>mdi-arrow-up</v-icon>
        </v-btn>
        <v-btn fab small dark color="primary" @click="selectNextRightArm" class="next-selector">
          <v-icon>mdi-arrow-down</v-icon>
        </v-btn>
      </div>
    </div>
    <div class="bottom-row">
      <div class="bottom part">
        <img v-bind:src="availableParts.bases[ selectNextBottomIndex ].src" title="bottom"/>
        <v-btn fab small dark color="primary" @click="selectPrevBottom" class="prev-selector">
          <v-icon>mdi-arrow-left</v-icon>
        </v-btn>
        <v-btn fab small dark color="primary"  @click="selectNextBottom" class="next-selector">
          <v-icon>mdi-arrow-right</v-icon>
        </v-btn>
      </div>
    </div>
    <div>
        <v-btn rounded color='primary'>Push Me</v-btn>
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
.prev-up {
  position: absolute;
  z-index:1;
  top: 10px;
  left: -45px;

}

.next-up {
  position: absolute;
  z-index:1;
  top: 10px;
  right: -45px;

}

.next-selector {
  position: absolute;
  z-index:1;
  top: 130px;
  right: -45px;
}

.center .prev-selector, .center .next-selector {
  opacity:0.8;
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
.right .prev-selector {
  top: 30px;
  left: 180px;  
}
.right .next-selector {
  top: auto;
  bottom: -45px;
  left: 130px;    
}
.right .next-selector {
  right: -3px;
}

</style>