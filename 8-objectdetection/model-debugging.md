# 🐞 Model Debugging

🙄 Problems that we can face while training custom object detection

1. Model is not doing well on test set
2. Model is doing well on test set but doing bad on real world images

In case that model is **not** doing well on test set you can try one or more from the followings:

* Add dropout to `.config` file

```javascript
box_predictor {
    ....
    use_dropout: true
    dropout_keep_probability: 0.8
    ....
}
```

* Replace `fixed_shape_resizer` with `keep_aspect_ratio_resizer`, example:

{% tabs %}
{% tab title="🖼 Before" %}
```javascript
image_resizer {
    fixed_shape_resizer {
    height: 640
    width: 640
  }
}
```
{% endtab %}

{% tab title="➰ After" %}
```javascript
keep_aspect_ratio_resizer {
    min_dimension: 640
    max_dimension: 640
    pad_to_max_dimension: true
}
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
👮‍♀️ You have to choose these values due to your model
{% endhint %}

