<template>
      <div>
    <div class="top-row">
      <div class="top part">
        <img v-bind:src="availableParts.heads[ selectNextHeadIndex ].src" title="head"/>
        <button @click="selectPreviousHead()" class="prev-selector">&#9668;</button>
        <button @click="selectNextHead()" class="next-selector">&#9658;</button>
      </div>
    </div>
    <div class="middle-row">
      <div class="left part">
        <img v-bind:src="availableParts.arms[ selectNextLeftArmIndex ].src" title="left arm"/>
        <button @click="selectPreviousLeftArm" class="prev-selector">&#9650;</button>
        <button @click="selectNextLeftArm" class="next-selector">&#9660;</button>
      </div>
      <div class="center part">
        <img v-bind:src="availableParts.torsos[selectNextTorsoIndex].src" title="torso"/>
        <button @click="selectPrevTorso" class="prev-selector">&#9668;</button>
        <button @click="selectNextTorso" class="next-selector">&#9658;</button>
      </div>
      <div class="right part">
        <img v-bind:src="availableParts.arms[ selectNextRightArmIndex ].src" title="right arm"/>
        <button @click="selectPrevRightArm" class="prev-selector">&#9650;</button>
        <button @click="selectNextRightArm" class="next-selector">&#9660;</button>
      </div>
    </div>
    <div class="bottom-row">
      <div class="bottom part">
        <img v-bind:src="availableParts.bases[ selectNextBottomIndex ].src" title="bottom"/>
        <button @click="selectPrevBottom" class="prev-selector">&#9668;</button>
        <button @click="selectNextBottom" class="next-selector">&#9658;</button>
      </div>
    </div>
  </div>
</template>

<script>
import availableParts from '../data/parts';

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
  border: 3px solid #aaa;
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
  top: -3px;
  left: -28px;
  width: 25px;
  height: 171px;
}
.next-selector {
  position: absolute;
  z-index:1;
  top: -3px;
  right: -28px;
  width: 25px;
  height: 171px;
}
.center .prev-selector, .center .next-selector {
  opacity:0.8;
}
.left .prev-selector {
  top: -28px;
  left: -3px;
  width: 144px;
  height: 25px;
}
.left .next-selector {
  top: auto;
  bottom: -28px;
  left: -3px;    
  width: 144px;
  height: 25px;
}
.right .prev-selector {
  top: -28px;
  left: 24px;  
  width: 144px;
  height: 25px;
}
.right .next-selector {
  top: auto;
  bottom: -28px;
  left: 24px;    
  width: 144px;
  height: 25px;
}
.right .next-selector {
  right: -3px;
}

</style>