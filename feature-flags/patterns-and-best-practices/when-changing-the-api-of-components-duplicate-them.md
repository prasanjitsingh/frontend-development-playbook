# When Changing The API Of Components, Duplicate Them

If your change is going to modify the API of a component or introduce component params that are only relevant to the new code, consider duplicating the component. Sure, this might feel like extra duplicate code, but it’s only temporary and it makes it much easier to understand the logic flow of the code paths.



**Instead of:**

```js
{{#ko-text-editor
  isRichFormattingAvailable=(variation "rich-notes")
  onAttachFiles=(if (variation "rich-notes") (action "onAttachFiles"))
  placeholder=(t "generic.add_a_note")
  isErrored=isErrored
  allowFormatting=(variation "rich-notes")
  isNote=true
  onTextChanged=(action "dispatch" "setReplyContents")
  value=state.replyContents
as |editor|}}
  {{!-- snip --}}
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
{{else}}
  {{#ko-text-editor-old
    placeholder=(t "generic.add_a_note")
    isErrored=isErrored
    isNote=true
    onTextChanged=(action "dispatch" "setReplyContents")
    value=state.replyContents
  as |editor|}}
    {{!-- snip --}}
{{/if}}
```



