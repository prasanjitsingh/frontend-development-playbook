# When Duplicating Components, Respect The Original Component Name

If you do duplicate a component temporarily for the sake of feature flagging, ensure the "new" version keeps the existing component name and you rename the existing one to something else. This will make it easier when it comes time to delete the feature flag to just delete the old one. As opposed to deleting the old one then renaming the new one to the old name.



**Instead of:**

```js
{{#if (variation "rich-notes")}}
  {{#ko-text-editor-new
    onAttachFiles=(action "onAttachFiles")
    placeholder=(t "generic.add_a_note")
    isErrored=isErrored
    isNote=true
    onTextChanged=(action "dispatch" "setReplyContents")
    value=state.replyContents
  as |editor|}}
    {{!-- snip --}}
  {{/ko-text-editor-new}}
{{else}}
  {{#ko-text-editor
    placeholder=(t "generic.add_a_note")
    isErrored=isErrored
    isNote=true
    onTextChanged=(action "dispatch" "setReplyContents")
    value=state.replyContents
  as |editor|}}
    {{!-- snip --}}
  {{/ko-text-editor}}
{{/if}}
```



**Consider:**

```js
{{#if (variation "rich-notes")}}
  {{#ko-text-editor
    onAttachFiles=(action "onAttachFiles")
    placeholder=(t "generic.add_a_note")
    isErrored=isErrored
    isNote=true
    onTextChanged=(action "dispatch" "setReplyContents")
    value=state.replyContents
  as |editor|}}
    {{!-- snip --}}
  {{/ko-text-editor}}
{{else}}
  {{#ko-text-editor-old
    placeholder=(t "generic.add_a_note")
    isErrored=isErrored
    isNote=true
    onTextChanged=(action "dispatch" "setReplyContents")
    value=state.replyContents
  as |editor|}}
    {{!-- snip --}}
  {{/ko-text-editor-old}}
{{/if}}
```



