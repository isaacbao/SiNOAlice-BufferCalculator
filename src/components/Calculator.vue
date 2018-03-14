<template>
  <div>
    <h1>{{ debuffEffectTitle }}</h1>
    <table border="1" class="result-table" id="debuff-effect">
      <tr>
        <td colspan="2">攻debuff</td>
        <td colspan="2">防debuff</td>
      </tr>
      <tr>
        <td colspan="2">100</td>
        <td colspan="2">100</td>
      </tr>
      <tr>
        <td colspan="1">物攻debuff</td>
        <td colspan="1">魔攻debuff</td>
        <td colspan="1">物防debuff</td>
        <td colspan="1">魔防debuff</td>
      </tr>
      <tr>
        <td colspan="1" id="physic-ATK-effect">50</td>
        <td colspan="1" id="magic-ATK-effect">50</td>
        <td colspan="1" id="physic-DEF-effect">50</td>
        <td colspan="1" id="magic-DEF-effect">50</td>
      </tr>
    </table>
  </div>
</template>

<script>
  const bookActiveSkillDatabase = {
    debuffLMagicATK10: {
      name: "衰弱ノ呪詛(Ⅳ)",
      description: "单体、魔攻",
      sp: 18,
      type:"debuff",
      effectMin: {physicATK: 0, magicATK: 0.054, physicDEF: 0, magicDEF: 0},
      effectExpectation: {physicATK: 0, magicATK: 0.054, physicDEF: 0, magicDEF: 0},
      effectMax: {physicATK: 0, magicATK: 0.054, physicDEF: 0, magicDEF: 0}
    },
    debuffLMagicATK15: {
      name: "衰弱ノ呪術(Ⅲ)",
      description: "1~2体、魔攻",
      sp: 21,
      type:"debuff",
      effectMin: {physicATK: 0, magicATK: 0.044, physicDEF: 0, magicDEF: 0},
      effectExpectation: {physicATK: 0, magicATK: 0.066, physicDEF: 0, magicDEF: 0},
      effectMax: {physicATK: 0, magicATK: 0.088, physicDEF: 0, magicDEF: 0}
    },
    debuffLMagicATK20: {
      name: "衰弱ノ呪術(Ⅱ)",
      description: "2体、魔攻",
      sp: 25,
      type:"debuff",
      effectMin: {physicATK: 0, magicATK: 0.072, physicDEF: 0, magicDEF: 0},
      effectExpectation: {physicATK: 0, magicATK: 0.072, physicDEF: 0, magicDEF: 0},
      effectMax: {physicATK: 0, magicATK: 0.072, physicDEF: 0, magicDEF: 0}
    },
    debuffLMagicATKDEF15: {
      name: "破魔ノ呪術(Ⅲ)",
      description: "1~2体、魔防魔攻",
      sp: 22,
      type:"debuff",
      effectMin: {physicATK: 0, magicATK: 0.044, physicDEF: 0, magicDEF: 0.072},
      effectExpectation: {physicATK: 0, magicATK: 0.066, physicDEF: 0, magicDEF: 0.108},
      effectMax: {physicATK: 0, magicATK: 0.088, physicDEF: 0, magicDEF: 0.144}
    },
    debuffLPhysicATK10: {
      name: "刀錆ノ呪詛(Ⅳ)",
      description: "单体、物攻",
      sp: 18,
      type:"debuff",
      effectMin: {physicATK: 0.054, magicATK: 0, physicDEF: 0, magicDEF: 0},
      effectExpectation: {physicATK: 0.054, magicATK: 0, physicDEF: 0, magicDEF: 0},
      effectMax: {physicATK: 0.054, magicATK: 0, physicDEF: 0, magicDEF: 0}
    },
    debuffLPhysicATKDEF10: {
      name: "枷鎖ノ呪詛(Ⅲ)",
      description: "单体、物攻物防",
      sp: 19,
      type:"debuff",
      effectMin: {physicATK: 0.049, magicATK: 0, physicDEF: 0.088, magicDEF: 0},
      effectExpectation: {physicATK: 0.049, magicATK: 0, physicDEF: 0.088, magicDEF: 0},
      effectMax: {physicATK: 0.049, magicATK: 0, physicDEF: 0.088, magicDEF: 0}
    },
    debuffLAllATK15: {
      name: "腐蝕ノ呪術(Ⅲ)",
      description: "1~2体、物攻魔攻",
      sp: 22,
      type:"debuff",
      effectMin: {physicATK: 0.044, magicATK: 0.044, physicDEF: 0, magicDEF: 0},
      effectExpectation: {physicATK: 0.066, magicATK: 0.066, physicDEF: 0, magicDEF: 0},
      effectMax: {physicATK: 0.088, magicATK: 0.088, physicDEF: 0, magicDEF: 0}
    },
    debuffLAllATK10: {
      name: "腐蝕ノ呪詛(Ⅲ)",
      description: "1体、物攻魔攻",
      sp: 18,
      type:"debuff",
      effectMin: {physicATK: 0.051, magicATK: 0.051, physicDEF: 0, magicDEF: 0},
      effectExpectation: {physicATK: 0.051, magicATK: 0.051, physicDEF: 0, magicDEF: 0},
      effectMax: {physicATK: 0.051, magicATK: 0.051, physicDEF: 0, magicDEF: 0}
    },
    debuffLAllDEF10: {
      name: "落城ノ呪詛(Ⅲ)",
      description: "单体、物防魔防",
      sp: 19,
      type:"debuff",
      effectMin: {physicATK: 0, magicATK: 0, physicDEF: 0.088, magicDEF: 0.088},
      effectExpectation: {physicATK: 0, magicATK: 0, physicDEF: 0.088, magicDEF: 0.088},
      effectMax: {physicATK: 0, magicATK: 0, physicDEF: 0.088, magicDEF: 0.088}
    },
    debuffLAllDEF15: {
      name: "落城ノ呪術(Ⅲ)",
      description: "1~2体、物防魔防",
      sp: 22,
      type:"debuff",
      effectMin: {physicATK: 0, magicATK: 0, physicDEF: 0.072, magicDEF: 0.072},
      effectExpectation: {physicATK: 0, magicATK: 0, physicDEF: 0.108, magicDEF: 0.108},
      effectMax: {physicATK: 0, magicATK: 0, physicDEF: 0.144, magicDEF: 0.144}
    },
    debuffLPhysicDEF20: {
      name: "壊壁ノ呪術(Ⅱ)",
      description: "2体、物防",
      sp: 25,
      type:"debuff",
      effectMin: {physicATK: 0, magicATK: 0, physicDEF: 0.124, magicDEF: 0},
      effectExpectation: {physicATK: 0, magicATK: 0, physicDEF: 0.124, magicDEF: 0},
      effectMax: {physicATK: 0, magicATK: 0, physicDEF: 0.124, magicDEF: 0}
    },
    debuffLPhysicDEF15: {
      name: "壊壁ノ呪術(Ⅲ)",
      description: "1~2体、物防",
      sp: 21,
      type:"debuff",
      effectMin: {physicATK: 0, magicATK: 0, physicDEF: 0.079, magicDEF: 0},
      effectExpectation: {physicATK: 0, magicATK: 0, physicDEF: 0.1135, magicDEF: 0},
      effectMax: {physicATK: 0, magicATK: 0, physicDEF: 0.158, magicDEF: 0}
    },
    debuffLPhysicDEF10: {
      name: "壊壁ノ呪詛(Ⅳ)",
      description: "单体、物防",
      sp: 18,
      type:"debuff",
      effectMin: {physicATK: 0, magicATK: 0, physicDEF: 0.095, magicDEF: 0},
      effectExpectation: {physicATK: 0, magicATK: 0, physicDEF: 0.095, magicDEF: 0},
      effectMax: {physicATK: 0, magicATK: 0, physicDEF: 0.095, magicDEF: 0}
    },
    debuffLMagicDEF20: {
      name: "解魔ノ呪術(Ⅱ)",
      description: "2体、魔防",
      sp: 25,
      type:"debuff",
      effectMin: {physicATK: 0, magicATK: 0, physicDEF: 0, magicDEF: 0.124},
      effectExpectation: {physicATK: 0, magicATK: 0, physicDEF: 0, magicDEF: 0.124},
      effectMax: {physicATK: 0, magicATK: 0, physicDEF: 0, magicDEF: 0.124}
    },
    debuffLMagicDEF15: {
      name: "解魔ノ呪術(Ⅲ)",
      description: "1~2体、魔防",
      sp: 21,
      type:"debuff",
      effectMin: {physicATK: 0, magicATK: 0, physicDEF: 0, magicDEF: 0.079},
      effectExpectation: {physicATK: 0, magicATK: 0, physicDEF: 0, magicDEF: 0.1135},
      effectMax: {physicATK: 0, magicATK: 0, physicDEF: 0, magicDEF: 0.158}
    },
    debuffLMagicDEF10: {
      name: "解魔ノ呪詛(Ⅳ)",
      description: "单体、魔防",
      sp: 18,
      type:"debuff",
      effectMin: {physicATK: 0, magicATK: 0, physicDEF: 0, magicDEF: 0.095},
      effectExpectation: {physicATK: 0, magicATK: 0, physicDEF: 0, magicDEF: 0.095},
      effectMax: {physicATK: 0, magicATK: 0, physicDEF: 0, magicDEF: 0.095}
    },
    buffLPhysicATK10: {
      name: "戦士の円舞曲(Ⅳ)",
      description: "单体、物攻",
      sp: 18,
      type:"buff",
      effectMin: {physicATK: 0.054, magicATK: 0, physicDEF: 0, magicDEF: 0},
      effectExpectation: {physicATK: 0.054, magicATK: 0, physicDEF: 0, magicDEF: 0},
      effectMax: {physicATK: 0.054, magicATK: 0, physicDEF: 0, magicDEF: 0}
    },
    buffLPhysicATK175: {
      name: "戦士の哀歌(Ⅳ)",
      description: "单体、物攻",
      sp: 22,
      type:"buff",
      effectMin: {physicATK: 0.054, magicATK: 0, physicDEF: 0, magicDEF: 0},
      effectExpectation: {physicATK: 0.0945, magicATK: 0, physicDEF: 0, magicDEF: 0},
      effectMax: {physicATK: 0.135, magicATK: 0, physicDEF: 0, magicDEF: 0}
    },
    buffLMagicATK10: {
      name: "魔術師の円舞曲(Ⅳ)",
      description: "单体、魔攻",
      sp: 18,
      type:"buff",
      effectMin: {physicATK: 0, magicATK: 0.54, physicDEF: 0, magicDEF: 0},
      effectExpectation: {physicATK: 0, magicATK: 0.54, physicDEF: 0, magicDEF: 0},
      effectMax: {physicATK: 0, magicATK: 0.54, physicDEF: 0, magicDEF: 0}
    },
    buffLPhysicATK175: {
      name: "魔術師の哀歌(Ⅳ)\n",
      description: "单体、魔攻",
      sp: 22,
      type:"buff",
      effectMin: {physicATK: 0, magicATK: 0.054, physicDEF: 0, magicDEF: 0},
      effectExpectation: {physicATK: 0, magicATK: 0.0945, physicDEF: 0, magicDEF: 0},
      effectMax: {physicATK: 0, magicATK: 0.135, physicDEF: 0, magicDEF: 0}
    },
  };

  const PASSIVE_SKILL_TYPE = {
    BUFF_UP: "buffUp",
    STATUS_UP: "status_up",
    GAY: "gay"
  };
  const PASSIVE_SKILL = {
    buffUp10: {
      name: "補助支援(壱)",
      type: PASSIVE_SKILL_TYPE.BUFF_UP,
      basicEffect: {max: 0.1, expectation: 0.1, min: 0.1}
    },
    buffUp20: {
      name: "補助支援(弐)",
      type: PASSIVE_SKILL_TYPE.BUFF_UP,
      basicEffect: {max: 0.2, expectation: 0.2, min: 0.2}
    },
    buffUp25: {
      name: "起死回生(弐)",
      type: PASSIVE_SKILL_TYPE.BUFF_UP,
      basicEffect: {max: 0.3, expectation: 0.25, min: 0.2}
    },
    buffUp30: {
      name: "起死回生(参)",
      type: PASSIVE_SKILL_TYPE.BUFF_UP,
      basicEffect: {max: 0.3, expectation: 0.3, min: 0.3}
    },
    physicATK20: {
      name: "刀刃展開(Ⅱ)",
      type: PASSIVE_SKILL_TYPE.STATUS_UP,
      effectMin: {physicATK: 0.0037, magicATK: 0, physicDEF: 0, magicDEF: 0},
      effectExpectation: {physicATK: 0.0111, magicATK: 0, physicDEF: 0, magicDEF: 0},
      effectMax: {physicATK: 0.0185, magicATK: 0, physicDEF: 0, magicDEF: 0}
    },
    magicATK10: {
      name: "方陣展開(Ⅰ)",
      type: PASSIVE_SKILL_TYPE.STATUS_UP,
      effectMin: {physicATK: 0, magicATK: 0.0027, physicDEF: 0, magicDEF: 0},
      effectExpectation: {physicATK: 0, magicATK: 0.0081, physicDEF: 0, magicDEF: 0},
      effectMax: {physicATK: 0, magicATK: 0.0135, physicDEF: 0, magicDEF: 0}
    },
    allATK20: {
      name: "武器補修(Ⅱ)",
      type: PASSIVE_SKILL_TYPE.STATUS_UP,
      effectMin: {physicATK: 0.0033, magicATK: 0.0033, physicDEF: 0, magicDEF: 0},
      effectExpectation: {physicATK: 0.0099, magicATK: 0.0099, physicDEF: 0, magicDEF: 0},
      effectMax: {physicATK: 0.0165, magicATK: 0.0165, physicDEF: 0, magicDEF: 0}
    },
    physicDEF10: {
      name: "鉄盾展開(Ⅰ)",
      type: PASSIVE_SKILL_TYPE.STATUS_UP,
      effectMin: {physicATK: 0, magicATK: 0, physicDEF: 0.004, magicDEF: 0},
      effectExpectation: {physicATK: 0, magicATK: 0, physicDEF: 0.012, magicDEF: 0},
      effectMax: {physicATK: 0, magicATK: 0, physicDEF: 0.02, magicDEF: 0}
    },
    physicDEF20: {
      name: "鉄盾展開(Ⅱ)",
      type: PASSIVE_SKILL_TYPE.STATUS_UP,
      effectMin: {physicATK: 0, magicATK: 0, physicDEF: 0.006, magicDEF: 0},
      effectExpectation: {physicATK: 0, magicATK: 0, physicDEF: 0.018, magicDEF: 0},
      effectMax: {physicATK: 0, magicATK: 0, physicDEF: 0.03, magicDEF: 0}
    },
    allDEF10: {
      name: "防具補修(Ⅰ)",
      type: PASSIVE_SKILL_TYPE.STATUS_UP,
      effectMin: {physicATK: 0, magicATK: 0, physicDEF: 0.004, magicDEF: 0.004},
      effectExpectation: {physicATK: 0, magicATK: 0, physicDEF: 0.012, magicDEF: 0.012},
      effectMax: {physicATK: 0, magicATK: 0, physicDEF: 0.02, magicDEF: 0.02}
    },
    allDEF20: {
      name: "防具補修(Ⅱ)",
      type: PASSIVE_SKILL_TYPE.STATUS_UP,
      effectMin: {physicATK: 0, magicATK: 0, physicDEF: 0.006, magicDEF: 0.006},
      effectExpectation: {physicATK: 0, magicATK: 0, physicDEF: 0.018, magicDEF: 0.018},
      effectMax: {physicATK: 0, magicATK: 0, physicDEF: 0.03, magicDEF: 0.03}
    },
    mahouGay10: {
      name: "魔力供給(壱)",
      type: PASSIVE_SKILL_TYPE.GAY,
      effect:0.8
    },
    mahouGay20: {
      name: "魔力供給(弐)",
      type: PASSIVE_SKILL_TYPE.GAY,
      effect:0.7
    }

  };

  export default {
    name: 'Calculator',
    data() {
      return {
        debuffEffectTitle: 'debuff总览'
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  table {
    align: center;
  }

</style>
