<template>
  <div>
    <div class="top-row">
      <div class="top part">
        <img :src="selectedRobot.head.src" title="head"/>
        <button @click="selectPreviousHead()" class="prev-selector">&#9668;</button>
        <button @click="selectNextHead()" class="next-selector">&#9658;</button>
      </div>
    </div>
    <div class="middle-row">
      <div class="left part">
        <img :src="selectedRobot.leftArm.src" title="left arm"/>
        <button @click="selectPreviousLeftArm()" class="prev-selector">&#9650;</button>
        <button @click="selectNextLeftArm()" class="next-selector">&#9660;</button>
      </div>
      <div class="center part">
        <img :src="selectedRobot.torso.src" title="left arm"/>
        <button @click="selectPreviousTorso()" class="prev-selector">&#9668;</button>
        <button @click="selectNextTorso()" class="next-selector">&#9658;</button>
      </div>
      <div class="right part">
        <img :src="selectedRobot.rightArm.src" title="left arm"/>
        <button @click="selectPreviousRightArm()" class="prev-selector">&#9650;</button>
        <button @click="selectNextRightArm()" class="next-selector">&#9660;</button>
      </div>
    </div>
    <div class="bottom-row">
      <div class="bottom part">
        <img :src="selectedRobot.base.src" title="left arm"/>
        <button @click="selectPreviousBase()" class="prev-selector">&#9668;</button>
        <button @click="selectNextBase()" class="next-selector">&#9658;</button>
      </div>
    </div>
  </div>
</template>

<script>
import parts from '../data/parts';


function getNextValidIndex(index, length) {
  const incrementedIndex = index + 1;
  return incrementedIndex > length - 1 ? 0 : incrementedIndex;
}
function getPreviousValidIndex(index, length) {
  const deprecatedIndex = index - 1;
  return deprecatedIndex < 0 ? length - 1 : deprecatedIndex;
}


export default {
  name: 'RobotBuilder',
  data() {
    return {
      parts,
      headIndex: 0,
      rightArmIndex: 0,
      leftArmIndex: 0,
      baseIndex: 0,
      torsoIndex: 0,
    };
  },
  methods: {
    selectNextHead() {
      this.headIndex = getNextValidIndex(this.headIndex, parts.heads.length);
    },
    selectPreviousHead() {
      this.headIndex = getPreviousValidIndex(this.headIndex, parts.heads.length);
    },
    selectPreviousLeftArm() {
      this.leftArmIndex = getPreviousValidIndex(this.leftArmIndex, parts.arms.length);
    },
    selectNextLeftArm() {
      this.leftArmIndex = getNextValidIndex(this.leftArmIndex, parts.arms.length);
    },
    selectPreviousTorso() {
      this.torsoIndex = getPreviousValidIndex(this.torsoIndex, parts.torsos.length);
    },
    selectNextTorso() {
      this.torsoIndex = getNextValidIndex(this.torsoIndex, parts.torsos.length);
    },
    selectPreviousRightArm() {
      this.rightArmIndex = getPreviousValidIndex(this.rightArmIndex, parts.arms.length);
    },
    selectNextRightArm() {
      this.rightArmIndex = getNextValidIndex(this.rightArmIndex, parts.arms.length);
    },
    selectNextBase() {
      this.baseIndex = getNextValidIndex(this.baseIndex, parts.bases.length);
    },
    selectPreviousBase() {
      this.baseIndex = getPreviousValidIndex(this.baseIndex, parts.bases.length);
    },

  },
  computed: {
    selectedRobot() {
      return {
        head: parts.heads[this.headIndex],
        leftArm: parts.arms[this.leftArmIndex],
        rightArm: parts.arms[this.rightArmIndex],
        torso: parts.torsos[this.torsoIndex],
        base: parts.bases[this.baseIndex],
      };
    },
  },
};
</script>

<style>
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
