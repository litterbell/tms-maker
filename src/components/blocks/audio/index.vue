<script>
import { h, ref } from 'vue'
import useComponentCommon from '@/hooks/useComponentCommon'

export default {
  name: 'blocks-audio',
  props: {
    config: {
      type: Object,
      required: true
    }
  },
  inject: ['mode'],
  setup (props) {
    const audioRef = ref('')
    const {
      computedStyle,
      mode
    } = useComponentCommon(props.config)
    const handleClick = () => {
      if (mode === 'pc') {
        return audioRef.value.pause()
      }
      if (audioRef.value.paused) {
        audioRef.value.play()
      } else {
        audioRef.value.pause()
      }
    }
    return () => h('div', {
      id: props.config.id,
      style: computedStyle(props.config),
      className: 'svg-icon'
    }, [
     
      h('audio', {
        controls: false,
        autoplay: true,
        loop: true,
        src: props.config.src,
        ref: audioRef
      }, [h('source', {
        src: props.config.src
      })])
    ])
  }
}
</script>

<style lang="scss" scoped>
@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

.svg-icon {
  animation: spin 1s linear infinite;
}
</style>
