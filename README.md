Description
This Liquid code snippet is designed for Shopify themes to display product variants based on their colors and sizes. It checks if the product has only a default variant and, if not, it lists out the variants categorized by color. The code ensures that all unique variants associated with each color are displayed, including the variant sizes and their IDs.

Explanation
Condition Check: {%- unless product.has_only_default_variant -%}

This checks if the product has more than the default variant. If true, the code inside the block is executed.
Container Div: <div class="color-and-size">

A container div with the class color-and-size is created to wrap the content.
Assign Color Options:

liquid
Copy code
{% assign color_options = product.options_with_values | where: 'name', 'Color' | map: 'values' | first %}
This line filters the product options to get the values where the option name is "Color" and assigns these values to color_options.
Outer Loop (Colors):

liquid
Copy code
{% for color in color_options %}
Iterates through each color in color_options.
Unordered List:

liquid
Copy code
<ul class="{{ color }}-variants">
For each color, an unordered list is created with a class named after the color followed by -variants.
Label:

liquid
Copy code
<label>{{ color }}:</label>
A label displaying the color name.
Assign Variants:

liquid
Copy code
{% assign option3_variants = product.variants | where: 'option3', color %}
{% assign option2_variants = product.variants | where: 'option2', color %}
{% assign all_variants = product.variants | where: 'option1', color | concat: option2_variants | concat: option3_variants | uniq %}
option3_variants: Filters the product variants where option3 matches the current color.
option2_variants: Filters the product variants where option2 matches the current color.
all_variants: Combines the variants filtered by option1, option2, and option3 that match the current color. The uniq filter ensures that only unique variants are included.
Inner Loop (Variants):

liquid
Copy code
{% for variant in all_variants %}
Iterates through each variant in all_variants.
List Item for Variant:

liquid
Copy code
<li>[{{ variant.option2 }} - Variant ID: {{ variant.id }}]</li>
Displays the size (assuming it is stored in option2) and the variant ID.
Close Tags:

The loops and div tags are properly closed.
Usage
This code can be added to your Shopify product template or a specific section where you want to display the variants organized by color and size. It enhances the user experience by providing a clear and structured view of the available product options.

Example Output
For a product with color options "Red" and "Blue" and size options "Small" and "Medium", the output would look like this:

html
Copy code
<div class="color-and-size">
  <ul class="Red-variants">
    <label>Red:</label>
    <li>[Small - Variant ID: 123456]</li>
    <li>[Medium - Variant ID: 123457]</li>
  </ul>
  <ul class="Blue-variants">
    <label>Blue:</label>
    <li>[Small - Variant ID: 123458]</li>
    <li>[Medium - Variant ID: 123459]</li>
  </ul>
</div>
This ensures that customers can easily see which sizes are available for each color variant of the product.
