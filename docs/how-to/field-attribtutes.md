# Atrributes of a Field


```TypeScript

class FieldModel {
  key: string;
  type?: string;

  label?: string;
  showLabel?: boolean = true;
  description?: string;
  icon?: string;
  placeholder?: string;
  style?: any;
  class?: string;

  permissions?: any[];

  value?: any | {
    value?: any,
    default?: any,
    key?: string,
    label?: string
  };

  readonly?: boolean;
  template?: string;
  format?: string;
  isHidden?: boolean;

  config?: any = {};

// for editing a field
  group?: any;
  control?: string;

  required?: boolean;
  validations?: any[];

// for rendring from db column
  dbKey: string;
  ascending?: boolean;
  formula?: string;

  filters?: any;
  showFilters?: any;
  isSticky?: boolean;

  isEmit?: boolean;
  click?: any;

  identity?: boolean;

  keys?: string[];
  values?: string[];
```