## Custom Widget
- source_model attribute maps to the model
-   **class**  : Defines the widget class
-   **id** : Gives custom widget an unique id

In widget node there are child nodes such as:

-   **label** : Sets the widget label that will appear in the widget list
-   **description**  : Sets widget description
-   **parameters** :  The parameters node allows you to add different parameters like the text, select, multiselect, block and templates. We will discuss further about this later in this tutorial.

**Widget Declaration**
```
<?xml version="1.0" ?>  
<widgets xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:samplewidget:Magento_Widget:etc/widget.xsd">  
 <widget class="Codilar\SampleWidget\Block\Widget\Posts" id="codilar_samplewidget_posts">  
        <label>Blog Posts</label>  
        <description>Posts</description>  
        <parameters>  
            <parameter name="posts" sort_order="10" visible="true" xsi:type="text">  
                <label>Sample Posts Label</label>  
            </parameter>  
        </parameters>  
    </widget>  
</widgets>
```

Add dependency in **module.xml**

```
<?xml version="1.0"?>  
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">  
    <module name="Codilar_SampleWidget"/>  
    <sequence>  
        <module name="Magento_Theme"/>  
        <module name="Magento_Cms" />  
        <module name="Magento_Widget"/>  
    </sequence>  
</config>
```
create a widget Block class **Posts.php**
```
namespace Codilar\SampleWidget\Block\Widget;  
  
use Magento\Framework\View\Element\Template;  
use Magento\Widget\Block\BlockInterface;  
  
class Posts extends Template implements BlockInterface  
{  
    protected $_template = "widget/posts.phtml";  
}
```
In the above snippet, **$_template** is used to set the template for the widget.

create a widget template file
```
<?php /** @var $block Codilar\SampleWidget\Block\Widget\Posts */  
if ($block->getData('posts')): ?>  
  <h2 class='posts'><?php echo $block->getData('posts'); ?></h2>  
    <p>This is sample widget. Perform your code here.</p>  
<?php endif; ?>
```

-   Now need to clear all the caches from the backend of Magento or delete folder **_var/cache_**.
-   go to **Administrator Page => Content => Pages** and add a new Page using Add New page button, then click Widget icon in Content Tab and you need fill information for all fields.
-   Save CMS page and go to the front end of page to **check  widget**.
