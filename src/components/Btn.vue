<template>
  <button id="customBtn" class="button" :class="classBinding" :disabled="disabled">Button
  </button>
</template>

<script>
export default {
  name: "Btn",
  props: {
    color: {
      type: String,
      default: "default",
      validator: function (value) {
        const colorValue = ['default', 'error', 'primary', 'secondary', 'warning', 'success'];
        if(!colorValue.includes(value)) {
          return 'default'
        }
        return value;
      }
      },
      disabled: {
        type: Boolean,
        default: false
      },
      block: {
        type: Boolean,
        default: false
      },
      large: {
        type: Boolean,
        default: false
      },
      small: {
        type: Boolean,
        default: false
      },
      elevation: {
        type: String,
        default: ""
      },
      text: {
        type: Boolean,
        default: false
      },
      fab: {
        type: Boolean,
        default: false
      },
      outlined: {
        type: Boolean,
        default: false
      },
      tile: {
        type: Boolean,
        default: false
      }
    },
    data() {
      return {}
    },
    computed: {
      classBinding() {
        return [
          this.color && `button__color--${this.color}`, this.block && 'button--block',
          this.large && 'button__size--large', this.small && 'button__size--small',
          parseInt(this.elevation)>0 && `button__shadow--${parseInt(this.elevation)}`,
          this.text && 'button__shape--text', this.fab && 'button__shape--fab',
          this.outlined && 'button__shape--outlined', this.tile && 'button__shape--tile'
        ];
      }
    },
  }
</script>

<style lang="scss" scoped>
$tw: 30px;
@mixin padding($sz) {
  padding: {
    left: $sz;
    right: $sz;
    top: $sz / 2;
    bottom: $sz / 2;
  };
}

@mixin color($bg-color, $bd-color, $color) {
  background-color: $bg-color !important;
  border-color: $bd-color !important;
  color: $color !important;
  &:hover {
    background-color: adjust-color($bg-color, $alpha: -0.3) !important;
  }
}

@mixin outlined-mode($color) {
  @include color(transparent, $color, $color);
  &:hover {
    background-color: adjust-color($color, $alpha: -0.95) !important;
  }
}

@mixin text-mode($color) {
  @include color(transparent, transparent, $color);
  &:hover {
    background-color: adjust-color($color, $alpha: -0.95) !important;
  }
}

.button {
  @include padding($tw);

  font: {
    size: $tw;
  }
  transition: all .3s;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  outline: 0;
  border: thin solid;
  border-radius: 5px;
  background-color: #f5f5f5;
  color: rgba(0, 0, 0, .87);
  cursor: pointer;

  &:disabled {
    cursor: default;
    color: rgba(0, 0, 0, .26) !important;
  }

  &__color--error {
    @include color(#ff5252, #ff5252, white);
  }

  &__color--primary {
    @include color(#1867c0, #1867c0, white);
  }

  &__color--secondary {
    @include color(#5cbbf6, #5cbbf6, white);
  }

  &__color--warning {
    @include color(#fb8c00, #fb8c00, white);
  }

  &__color--success {
    @include color(#4caf50, #4caf50, white);
  }

  &__display--block {
    display: block;
    width: 100%;
  }

  &__size--small {
    @include padding($tw - 10px);
    font: {
      size: $tw - 10px;
    }
  }

  &__size--large {
    @include padding($tw + 10px);
    font: {
      size: $tw;
    }
  }

  @for $i from 1 through 20 {
    &__shadow--#{$i} {
      box-shadow: 0 round($i/2)+px round($i/2)+1px -1*(round($i/2)-2)+px rgba(0, 0, 0, .2), 0 $i+px $i+px ($i/10)+px rgba(0, 0, 0, .14), 0 ($i/2-1)+px ($i*2)+px ($i/4)+px rgba(0, 0, 0, .12) !important;;
    }
  }

  &__shape--text {
    @include text-mode(rgba(0, 0, 0, .87));

    &.button__color--error {
      @include text-mode(#ff5252);
    }

    &.button__color--primary {
      @include text-mode(#1867c0);
    }

    &.button__color--secondary {
      @include text-mode(#5cbbf6);
    }

    &.button__color--warning {
      @include text-mode(#fb8c00);
    }

    &.button__color--success {
      @include text-mode(#4caf50);
    }
  }

  &__shape--outlined {
    @include outlined-mode(rgba(0, 0, 0, .87));

    &.button__color--error {
      @include outlined-mode(#ff5252);
    }

    &.button__color--primary {
      @include outlined-mode(#1867c0);
    }

    &.button__color--secondary {
      @include outlined-mode(#5cbbf6);
    }

    &.button__color--warning {
      @include outlined-mode(#fb8c00);
    }

    &.button__color--success {
      @include outlined-mode(#4caf50);
    }
  }

  &__shape--tile {
    border-radius: 0 !important;
  }

  &__shape--fab {
    @include padding($tw);
    height: 92px;
    width: 92px;
    border-radius: 50% !important;
  }
}
</style>
