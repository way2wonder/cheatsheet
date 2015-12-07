### 概述

1. 使用方式

2.


validate( [options ] )
  options:
  1. debug  : boolean
  2. submitHandler :   form  is  the only argument
```javascript
    function(form) 
    {
      $(form).ajaxSubmit();
    }
```
  3. invalidHandler   提交校验失败的表单触发的事件
     ex:
    ```
     invalidHandler: function(event, validator) {
    // 'this' refers to the form
    var errors = validator.numberOfInvalids();
    if (errors) {
      var message = errors == 1
        ? 'You missed 1 field. It has been highlighted'
        : 'You missed ' + errors + ' fields. They have been highlighted';
      $("div.error span").html(message);
      $("div.error").show();
    } else {
      $("div.error").hide();
    }
  }
  ```
  4. ignore   校验时候可以忽略的元素。使用了jquery的`not()`方法，所以
  not方法能传递的options 都可以传递
    ```
    $("#myform").validate({
       ignore: ".ignore"
    });

```
  5. rules(default: rules are read from markup (classes, attributes, data))

  6. rules中depends用法。一个规则的校验基于另外一个元素的校验状态。
    ```
    $(".selector").validate({
  rules: {
    // at least 15€ when bonus material is included
    pay_what_you_want: {
      required: true
      min: {
        // min needs a parameter passed to it
        param: 15,
        depends: function(element) {
          return $("#bonus-material").is(":checked");
        }
      }
    }
  }
});
```

  7. messages  
    ```
     messages: {
    name: "Please specify your name",
    email: {
      required: "We need your email address to contact you",
      email: "Your email address must be in the format of name@domain.com"
    }
  }
  ```
  中动态传入rules中参数的方式 ｛0｝


  8.  errorClass  validClass  errorElement
  9.   wrapper   errorLabelContainer
  ```
  $("#myform").validate({
  errorLabelContainer: "#messageBox",
  wrapper: "li",
  submitHandler: function() { alert("Submitted!") }
  });
 ```

###rules()方法，用于新增和删除元素的校验规则
ex:
   - romove:`$( "#myinput" ).rules( "remove", "min max" );`
   - add:
```
       $( "#myinput" ).rules( "add", {
  required: true,
  minlength: 2,
  messages: {
    required: "Required input",
    minlength: jQuery.validator.format("Please, at least {0} characters are necessary")
  }
});

```

###valid()方法，判断form或者元素校验是否通过
扩展的3个筛选器：  ：blank   ：filled  ：unchecked




###validator 对象
validator.form()  
validator.element()
validator.resetForm()
validator.showErrors()
validator.numOfInvalids()
ex:
```
var validator = $( "#myform" ).validate();
validator.form();
```


validator.addMethod(name,method,message)

name:校验方法名
method:参数有value，element,params
ex:
```
jQuery.validator.addMethod("math", function(value, element, params) {
  return this.optional(element) || value == params[0] + params[1];
}, jQuery.validator.format("Please enter the correct value for {0} + {1}"));

```



###jQuery.validator.setDefaults( options )
设置校验器默认的格式，和validate() 接收的参数一样

####两种方法：有什么不一样？
jQuery.validator.addClassRules( name, rules )
jQuery.validator.addClassRules(rules )







###required  (depend或者后面跟个函数返回true或者false）   
 
```
$( "#myform" ).validate({
  rules: {
    details: {
      required: "#other:checked"
    }
  }
});
```

##build-in validators

###build-in validator :remote

```
$( "#myform" ).validate({
  rules: {
    email: {
      required: true,
      email: true,
      remote: {
        url: "check-email.php",
        type: "post",
        data: {
          username: function() {
            return $( "#username" ).val();
          }
        }
      }
    }
  }
});
```

###build-in validator :equalTo   rangelength  range
###add-on validator:  accept  extension:扩展类型校验
###add-on validator: require_from_group 

```
$( "#myform" ).validate({
  rules: {
    mobile_phone: {
      require_from_group: [1, ".phone-group"]
    },
    home_phone: {
      require_from_group: [1, ".phone-group"]
    },
    work_phone: {
      require_from_group: [1, ".phone-group"]
    }
  }
});
```

三选一，有一项满足就可以



重写内置的校验器

```javascript

$.validator.methods.email = function( value, element ) {
  return this.optional( element ) || /[a-z]+@[a-z]+\.[a-z]+/.test( value );
}

```


