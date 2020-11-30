<script type="text/jsx">
import Antd from 'ant-design-vue'
import {Button} from 'ant-design-vue'
import {version} from 'ant-design-vue'
import PropTypes, {withUndefined} from 'ant-design-vue/lib/_util/vue-types/index'

export default {
  components: {},

  setup() {
    const components = []
    const fakeApp = {
      component: function (name, component) {
        components.push(component)
      },
      use: function (component) {
        component.install(fakeApp)
      },
      config: {
        globalProperties: {}
      },
    }
    Antd.install(fakeApp)

    const createTag = component => {
      // 只包含属性名称
      const attributes = []
      for (let key in component.props) {
        let type = 'string'
        const propTypeName = component.props[key]._vueTypes_name

        switch (propTypeName) {
          case PropTypes.looseBool._vueTypes_name:
            type = 'boolean'
            break
          case PropTypes.func._vueTypes_name:
            type = 'function'
            break
          case PropTypes.number._vueTypes_name:
            type = 'number'
            break
            // case PropTypes.oneOf._vueTypes_name:
            //   type =
          default:
            type = 'string'
            break
        }

        if (PropTypes)
          attributes.push({
            name: key,
            value: {
              kind: 'expression',
              type: type
            },
          })
      }

      return {
        name: component.name,
        attributes: attributes
      }
    }

    const tags = components.map(createTag)

    const webTypes = {
      $schema: 'http://json.schemastore.org/web-types',
      framework: 'vue',
      name: 'ant-design-vue',
      version: version,
      contributions: {
        html: {
          'types-syntax': 'typescript',
          'description-markup': 'markdown',
          tags,
        },
      },
    }

    const prettyResult = JSON.stringify(webTypes, null, 2)

    return () => (
        <div id="app">
          <div class="json">{prettyResult}</div>
        </div>
    )
  },
}
</script>
<style>
.json {
  white-space: pre;
}
</style>