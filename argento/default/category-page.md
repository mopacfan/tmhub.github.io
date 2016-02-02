---
layout: default
title: Argento Default theme Category Page
description: Argento Default category page
keywords: "Argento default, argento argento, category, listing, label, columns count"
category: Argento
---

# Argento Default theme Category Page

### Layout

Argento default theme is using `page_two_columns_right` layout for the category page. In order to
change it to another one you have to create [custom.xml][custom_xml] file with following
instruction:

```xml
<catalog_category_default>
    <update handle="page_two_columns_right"/>
</catalog_category_default>
<catalog_category_layered>
    <update handle="page_two_columns_right"/>
</catalog_category_layered>
```

Possible values for handle variable:

```
page_two_columns_left
page_two_columns_right
page_three_columns
page_one_column
```

### Category Description

![Collapsed category description](/images/argento/pure2/category-page/collapsed_description.png)

Category description is shown as collapsed block, when its height is longer than
250px. If you would like to disable description collapsing, you can add the following
code to [custom.xml][custom_xml]:
If you want remove "more" only for some specific categories, you have to remove custom.xml file. Then place "<remove name="collapsed_category_description"/>" code in textarea "Custom Layout Update" for category where you want to remove "more":

```xml
<remove name="collapsed_category_description"/>
```

## Product Listing

![Product Listing](/images/argento/default/category-page-product-list.jpg)

#### Columns count

Columns count can be configured with [custom.xml][custom_xml].
Add the following code to the custom.xml file:

```xml
<products_four_columns>
    <block type="catalog/product_list_toolbar" name="product_list_toolbar" template="catalog/product/list/toolbar.phtml">
        <block type="page/html_pager" name="product_list_toolbar_pager"/>

        <action method="setDefaultGridPerPage"><limit>4</limit></action>
        <action method="addPagerLimit"><mode>grid</mode><limit>4</limit></action>
        <action method="addPagerLimit"><mode>grid</mode><limit>8</limit></action>
        <action method="addPagerLimit"><mode>grid</mode><limit>12</limit></action>

        <action method="setDefaultListPerPage"><limit>4</limit></action>
        <action method="addPagerLimit"><mode>list</mode><limit>8</limit></action>
        <action method="addPagerLimit"><mode>list</mode><limit>16</limit></action>
        <action method="addPagerLimit"><mode>list</mode><limit>32</limit></action>
    </block>

    <reference name="product_list">
        <action method="setColumnCount"><columns>4</columns></action>
        <action method="setToolbarBlockName"><name>product_list_toolbar</name></action>
    </reference>
    <reference name="search_result_list">
        <action method="setColumnCount"><columns>4</columns></action>
        <action method="setToolbarBlockName"><name>product_list_toolbar</name></action>
    </reference>
</products_four_columns>

<catalog_category_layered>
    <update handle="products_four_columns"/>
</catalog_category_layered>
<catalog_category_default>
    <update handle="products_four_columns"/>
</catalog_category_default>
<catalogsearch_result_index>
    <update handle="products_four_columns"/>
</catalogsearch_result_index>
<catalogsearch_advanced_result>
    <update handle="products_four_columns"/>
</catalogsearch_advanced_result>
```

#### Image size

Follow the steps below to change the image's size on the category view page:

 1. Copy product list template to the `argento_custom` folder:

    ```
    cp app/design/frontend/argento/pure2/template/catalog/product/list.phtml app/design/frontend/argento/pure2_custom/template/catalog/product/list.phtml
    ```

 2. Change the image dimensions in copied file.

    Find the following lines:

    ```php
    <img id="product-collection-image-<?php echo $_product->getId(); ?>"
        src="<?php echo $this->helper('catalog/image')->init($_product, 'small_image')->keepFrame(false)->resize(270); ?>"
        srcset="<?php echo $this->helper('catalog/image')->init($_product, 'small_image')->keepFrame(false)->resize(270); ?> 1x, <?php echo $this->helper('catalog/image')->init($_product, 'small_image')->keepFrame(false)->resize(270 * 2); ?> 2x"
        alt="<?php echo $this->stripTags($this->getImageLabel($_product, 'small_image'), null, true) ?>"
    />
    ```

    Replace them with:

    ```php
    <img id="product-collection-image-<?php echo $_product->getId(); ?>"
        src="<?php echo $this->helper('catalog/image')->init($_product, 'small_image')->keepFrame(true)->resize(270, 270); ?>"
        srcset="<?php echo $this->helper('catalog/image')->init($_product, 'small_image')->keepFrame(true)->resize(270, 270); ?> 1x, <?php echo $this->helper('catalog/image')->init($_product, 'small_image')->keepFrame(true)->resize(270 * 2, 270 * 2); ?> 2x"
        alt="<?php echo $this->stripTags($this->getImageLabel($_product, 'small_image'), null, true) ?>"
    />
    ```

    Remember to make the same operation for the image in grid and list modes.

#### Product labels

The display of the label on product is powered by Prolabels module. You can add custom label or assign it to any items on the Category page at `Templates-Master > Prolabels` backend page.
