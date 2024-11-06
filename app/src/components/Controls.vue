<script setup>
import ControlItem from './ControlItem.vue'
import SkillIcon from './icons/IconSkill.vue'
import RollIcon from './icons/IconRoll.vue'
import RollButton from './Button.vue'

defineEmits( [ 'result-message' ] )
</script>

<template>
  <div>
    <ControlItem>
      <template #icon>
        <SkillIcon />
      </template>
      <template #heading>
        Skill
      </template>
      <v-slider v-model="skill" thumb-label="always" step="1" track-size="1"></v-slider>
    </ControlItem>

    <ControlItem>
      <template #icon>
        <RollIcon />
      </template>
      <template #heading>
        Roll
      </template>
      <v-slider v-model="roll" thumb-label="always" step="1" track-size="1"></v-slider>

    </ControlItem>

    <RollButton label="roll" @clicked="reroll" />
  </div>
</template>

<style></style>

<script>
export default {
  data()
  {
    return {
      skill: 50,
      roll: 0,
    }
  },
  watch: {
    skill: 'checkSuccess',
    roll: 'checkSuccess'
  },
  methods: {
    reroll()
    {
      console.log( 'reroll listener' )

      this.roll = Math.floor( Math.random() * ( 100 - 1 ) + 1 )
    },
    checkSuccess()
    {
      let isSuccess = this.roll <= this.skill
      let superiors = 0

      // check for crit
      let isCrit = [ 11, 22, 33, 44, 55, 66, 77, 88 ].includes( this.roll )

      // 99 always fails
      if ( this.roll == 99 ) {
        isCrit = true
        isSuccess = false
      }

      // 100 always fails
      if ( this.roll == 100 ) {
        isCrit = true
        isSuccess = true
      }

      // check for 33/66
      if ( isSuccess && this.roll >= 66 ) {
        superiors = 2
      }
      else if ( isSuccess && this.roll >= 33 ) {
        superiors = 1
      }
      else if ( !isSuccess && this.roll <= 33 ) {
        superiors = 2
      }
      else if ( !isSuccess && this.roll <= 66 ) {
        superiors = 1
      }

      /*console.log( 'skill', this.skill )
      console.log( 'roll', this.roll )
      console.log( 'isCrit', isCrit )
      console.log( 'success', isSuccess )
      console.log( 'superiors', superiors )*/

      this.writeResult( isCrit, isSuccess, superiors )

    },
    writeResult( isCrit, isSuccess, superiors )
    {
      let msg

      if ( isCrit ) {
        msg = isSuccess ? 'Critical Success!' : 'Critical Failure!'
      }
      else {
        if ( isSuccess ) {
          if ( superiors === 2 ) {
            msg = '2 Superior Successes'
          }
          else if ( superiors === 1 ) {
            msg = 'Superior Success'
          }
          else {
            msg = 'Success'
          }
        }
        else {
          if ( superiors === 2 ) {
            msg = '2 Superior Failures'
          }
          else if ( superiors === 1 ) {
            msg = 'Superior Failure'
          }
          else {
            msg = 'Failure'
          }
        }
      }

      //console.log( 'emitting result-message', msg )
      this.$emit( 'result-message', msg )
    }
  }
}
</script>