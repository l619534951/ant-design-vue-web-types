<script type="text/jsx">
import Antd from 'ant-design-vue'
import { version } from 'ant-design-vue'

export default {
  components: {  },

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
        attributes.push({
          name: key
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
          <div class="json">{ prettyResult }</div>
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