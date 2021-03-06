<template>
  <div
    :class="context.classes.element"
    :data-type="context.type"
    :data-multiple="attributes && attributes.multiple !== undefined"
  >
    <jt-select
      v-bind="attributes"
      v-on="$listeners"
      v-model="context.model"
      :options="context.options"
      @blur="context.blurHandler"
    >
      <template v-slot:label>
        <slot
          v-if="context.labelPosition === 'float'"
          name="label"
          v-bind="context"
        >
          <component
            :is="context.slotComponents.label"
            v-if="context.hasLabel"
            :context="context"
            v-bind="context.slotProps.label"
          />
        </slot>
      </template>
    </jt-select>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

type FormulateAttributes = {
  placeholder?: string;
}

type FormulateContext = {
  attributes: FormulateAttributes;
  type: string | boolean;
  hasValue: boolean;
  label: string | boolean;
  labelPosition: string | boolean;
}

@Component
export default class JtFormulateInputSelect extends Vue {
  @Prop({ required: true })
  private context!: FormulateContext;

  get type(): string | boolean {
    return this.context.type;
  }

  get attributes(): object {
    const attrs: FormulateAttributes = (this.context.attributes || {});
    if (this.context.labelPosition === 'float') {
      // Inject Label into Placeholder
      attrs.placeholder = typeof this.context.label === 'string'
        ? this.context.label
        : ' ';
    }
    return {
      ...this.$attrs,
      ...attrs,
    };
  }

  hasValue(): boolean {
    return this.context.hasValue;
  }
}
</script>
