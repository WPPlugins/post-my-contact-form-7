=== Post My CF7 Form ===
Contributors: aurovrata
Donate link: https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=DVAJJLS8548QY
Tags: contact form 7, contact form 7 module, post, custom post, form to post, contact form 7 to post, contact form 7 extension
Requires at least: 4.7
Tested up to: 4.8
Stable tag: 2.0.0
License: GPLv2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html

This plugin enables the mapping of your CF7 forms to custom posts, including featured images, files, meta-fields and taxonomies

== Description ==

This plugin enables the mapping of each form field to a post field.   Each forms submitted from your website will then be saved as a new post which you can manage in your dashboard and display on the front end.

You can submit and map to a post all of the following fields,

* Default post field, title, author, content, excerpt
* featured image, you can **submit a file** and save it as a post attachment
* meta fields, unlimited number of **meta-fields** can be created
* **taxonomies**, you can map select/checkbox/radio input fields to taxonomies
* map your submitted forms to **existing post types** using the new UI
* addition of form key to identify cf7 forms instead of the form id to make development more portable
* this plugin allows your users to manage multiple draft submissions from a single page.
* for large forms with multiple fields, an auto-create functionality has been added for meta-field mapping.  See the installation instruction for details.

= Make your CF7 Form more portable =

 this plugin introduces form keys (which you can modify in the CF7 admin table).  Keys are unique for each form, allowing you identify a form my its key rather than an ID.  Why is this priceless?  IDs changes from one server to the next because they are the custom post ID attributed by the WordPress installation, and therefore you develop your form in a local machine only to find out that the IDs are different when you move your form to your production server.  To overcome this problem, we suggest you use a form key along with this plugin's contact form shortcode, `[cf7-2-post key="contact-us"]`.  Don't worry your old contact form 7 shortcodes will still work too, behind the scenes we simply map the key to the ID and call the regular contact form 7 shortcode.


= Filters for fields =

In addition to mapping your form fields to post fields you are also given a custom filter for that specific form field.  The filter option allows you to custom fill the post created for the submitted form, for example if a form requests the date of birth, you may want to create an additional post field for the age, so you can filter the date field in your `functions.php` file and calculate the age and save it to a custom post meta field.  The custom filters are created using the following nomenclature, `cf7_2_post_filter-<post_type>-<post-field>`.  For example if you have created a custom post type `quick-contact`, which as a meta field `age`, you could filter it with,
`
add_filter('cf7_2_post_filter-quick-contact-age','filter_date_to_age',10,3);
function filter_date_to_age($value, $post_id, $form_data){
  //$value is the post field value to return, by default it is empty
  //$post_id is the ID of the post to which the form values are being mapped to
  // $form_data is the submitted form data as an array of field-name=>value pairs
  if(isset($form_data['date-of-birth']){
    //calculate the age
    $value = ....
  }
  return $value;
}
`
= Special Fields =

**Author** - unless the user sets the field, the default set in this order: current logged in user else, the recipient of the CF7 form email if such a user exists in the database, else it reverts to the user_id=1 which is the administrator.  A filter is also available to set the author.

**Featured image/Thumbnail** - these will only accept form fields of type *file*.  However, non image files uploaded will not show up as thumbnails in the post edit page.

**Title/Content/Excerpt** - there are enabled by default, and can be used to map any form fields to them.  However, if you wish disable these fields (using the post registration *supports* array of values), then please use the filter that allows these to be set for your custom post type.  (see the [filters section](https://wordpress.org/plugins/post-my-contact-form-7/other_notes/) for more info)

= Pre-fill form fields =

Contact Form 7 does not allow you to pre-fill fields before your form is displayed.  With this plugin you can do this, you will need to map your form first, and use the filter 'cf7_2_post_filter_cf7_field_value' to pre-fill your fields, see the [Filter & Actions](https://wordpress.org/plugins/post-my-contact-form-7/other_notes/) section for more details.

= Contact Form 7 list table =

This plugin re-organises the CF7 dashboard list table, using the cf7 custom post list table to permit other developpers to easily add custom columns to the list table.  You can therefore use [WP functionality](http://justintadlock.com/archives/2011/06/27/custom-columns-for-custom-post-types) to customise your table.  For example you could view how many submits a form has received.

= Other hooks =

The plugin has been coded with additional actions and filters to allow you to hook your functionality such as when a form to post mapping is completed.  For a list of such hooks, please refer to the [Filter & Actions](https://wordpress.org/plugins/post-my-contact-form-7/other_notes/) section.

= Checkout our other CF7 plugin extensions =

* [CF7 Polylang Module](https://wordpress.org/plugins/cf7-polylang/) - this plugin allows you to create forms in different languages for a multi-language website.  The plugin requires the [Polylang](https://wordpress.org/plugins/polylang/) plugin to be installed in order to manage translations.

* [CF7 Multi-slide Module](https://wordpress.org/plugins/cf7-multislide/) - this plugin allows you to build a multi-step form using a slider.  Each slide has cf7 form which are linked together and submitted as a single form.

* [Post My CF7 Form](https://wordpress.org/plugins/post-my-contact-form-7/) - this plugin allows you to save you cf7 form to a custom post, map your fields to meta fields or taxonomy.  It also allows you to pre-fill fields before your form  is displayed.

* [CF7 Google Map](https://wordpress.org/plugins/cf7-google-map/) - allows google maps to be inserted into a Contact Form 7.  Unlike other plugins, this one allows map settings to be done at the form level, enabling diverse maps to be configured for each forms.

== Installation ==

1. Install the *Contact Form 7* plugin
2. Install the *Post My CF7 Form* plugin
3. Create a contact form.  A new column appears in the contact table list which shows you which Post Type the form is mapped to
4. Click on the link 'Create New' that appears on the column to start mapping your form to a custom post.
5. Create the post and it will appear in your Dashboard.  Currently you cannot undo a mapped form, you will have to create a new form and re-map it while deleting the old one to change the mapping.  So be careful when you save finally create your form.  In a later version of this plugin I will introduce functionality to un-publish a mapped form.
6. As of v1.5 of this plugin a functionality has been introduced to quickly create meta-field mappings. This is useful when you have complex forms with multiple fields. Simply add a new meta-field and select a field to map (leave the meta field name to the default value), the meta-field name will automatically update itself to reflect the form field name with hyphens replaced by underscores. Subsequent additions of new meta-fields will further increase the magic by auto-selecting the next form field in the dropdown and filling in the meta-field name too.  If you wish to switch-off this functionality, simply manually edit the meta-field name and it will switch-off the autofill.
6. Each time a visitor submits the form on your website, a new post will be created.


== Frequently Asked Questions ==

= How do I map a form to a post? =

In the Contact Form 7 table list you will notice a new column has been added which allows you to create a new custom post mapping.  This will take you to a new screen where you will see your existing fields listed in select dropdowns.  Map your form fields to either a default field (eg title, content, excerpt, or author), or create a custom (meta) field, or even create a new taxonomy for your post.  Once you have mapped your form you can save it as a draft or publish it.  Once published you cannot edit the mapping anymore, so be warned.  As of version 1.2.0 you will have to delete the whole form and start again to remap it.  Subsequent versions may introduce a 'delete' button.

= How do I edit an existing mapping ? =
Existing 'published' mappings cannot be edited, you can only add new fields to them.

= How do remove a mapping? =
At this point it is not possible, you can either delete the form and start again, or if you can search your cf7 form ID's in the `wp_post_meta` table and edit the meta field '_cf7_2_post-map' to 'draft'.

= How do I map a field to a taxonomy ? =

You create a new taxonomy and map your field to it.  Note however that only select/checkbox/radio type of fields can be mapped to taxonomies.  Once mapped and published you will see your taxonomy appear in your custom post menu.  You can add terms to your taxonomy and these will be made pre-filled into your mapped field.  Users can select a term and when the form is submitted, the post will be created with those terms assigned to it.

= How do I create non-hierarchical taxonomies ? =

You need to use a special filter for this, 'cf7_2_post_filter_taxonomy_registration-{$taxonomy_slug}', see the [Filter & Actions](https://wordpress.org/plugins/post-my-contact-form-7/other_notes/) section for more details.

= Why filter the taxonomy mapping ? =
You may have noticed that in addition to mapping a post field or taxonomy to one of your form fields, you can also use a filter to hook your own custom values.  In the case of taxonomies, you can actually map a form submission to a specific set of terms depending on the submission of other fields.

= How do I allow my form users to create a new term for a taxonomy? =
This is a little more complex.  You will need to create an input field in your form in which users can submit a new term.  You will then need to hook the action `cf7_2_post_form_mapped_to_{$post_type}` which is fired right at the end of the saving process.  The hook parses the newly created `$post_ID` as well as the submitted `$cf7_form_data` form data array.  You can then check if your user has submitted a new value and [include it in taxonomy](https://codex.wordpress.org/Function_Reference/wp_insert_term) and [assign the new term to the post](https://codex.wordpress.org/Function_Reference/wp_set_object_terms).

= How can I pre-fill a form from a WordPress page template that contains a CF7 form ? =

This can be done using the `cf7_2_post_form_values` filter (see [Filter & Actions](https://wordpress.org/plugins/post-my-contact-form-7/other_notes/) for more details).  You will need to create an [anonymous function](http://php.net/manual/en/functions.anonymous.php) on this filter and pass the CF7 id form your shortcode which you can automatically scan for form your page content.  In the example below I assume that the page contains the default 'Contact Me' CF7 form which I want to pre-fill if a user is logged in,

`
$content = get_the_content();
//let's find our shortcode
preg_match_all( '/' . get_shortcode_regex() . '/s', $content, $matches );
$args = array();
if( isset( $matches[2] ) ){
  foreach( (array) $matches[2] as $key => $shortcode ){
    if( 'contact-form-7' === $shortcode )
      $args[] = shortcode_parse_atts( $matches[3][$key] );
  }
}
//here I am assuming there is a single form on the page, if you have multiple, you will need to loop though each one
if(!empty($args) && isset($args[0]['id'])){
  $short_id = $args[0]['id'];
  $values = array();

  if(is_user_logged_in()){
    $user = wp_get_current_user();
    $values['your-name']= $user->display_name;
    $values['your-email'] = $user->user_email;
    if(!empty($subject)){
      $term = get_term_by('id', $subject, 'project-type');
      $values['your-message'] = 'Dear Hexagon,'.PHP_EOL.'I request you to create a new '.rtrim($term->name,'s') ;

    }
    //now lets filter the values
    add_filter('cf7_2_post_form_values', function($field_values, $cf7_id) use ($short_id, $values){
      if($short_id == $cf7_id ){
        return $values;
      }
    }, 10,2);
  }
}
`
= How to use custom javascript script on the form front-end ? =

The plugin fires a number of jQuery scripts in order to map saved submissions back to draft forms.  So if you have a form which your users can save before submitting and you need to customise some additional functionality on your form on `$(document).ready()`, then you need to make sure it fires after the plugin's scripts have finished.  In order to achieve this, the script fires a custom event on the form, `cf7Mapped`, which you can use to ensure you script fires in the right order, here is how you would enable this,
`
(function( $ ) {
	'use strict';
  $( function() { //the jQuery equivalent of document.ready()
    var cf7Form = $('div.cf7_2_post form.wpcf7-form'); //this ensures you target the mapped forms
    cf7Form.on('formMapped', function(){
      //fire your script
    });
  });
})( jQuery );
`
= Is it possible to save my form to an existing post type? =

yes, but you need to know how to use WordPress hooks in your functions.php file in order to get it to work.  If you map your form, you now have a dropdown to select the type of post to which you want to save it to.  When you select 'Existing Post' from the option, instructions will show up on screen to map your form.

= I am saving my form to an existing post, can I pre-load taxonomy terms in my form? =

Sure you can, again you need to use the hooks `cf7_2_post_map_extra_taxonomy` & `cf7_2_post_pre_load-{$post_type}` to get it to work, see the example in the section [Filter & Actions](https://wordpress.org/plugins/post-my-contact-form-7/other_notes/).

= Is there any advanced documentation for developers ? =
sure, there is a section [Filter & Actions](https://wordpress.org/plugins/post-my-contact-form-7/other_notes/) which lists all the hooks (filters & actions) available for developers with examples of how to use them.  These expose a lot of the default functionality for further fine-tuning.  If you see a scope for improvement and/or come across a bug, please report it in the support forum.

= Is it possible to have multiple forms submitted from a single page ? =
yes, as of v1.4 of this plugin you can now have multiple saved/draft submissions on a single page.  To get it to work you need to track which forms are mapped to which post yourself.  Introduce a hidden variable in your form to store your mapped post ids.  For example you have a custom post which maps/stores submitted faults  reported by your users.  On  page load, you need to pass the mapped post id to this plugin via your cf7 shortcode by dynamically calling the shortcode using `do_shortcode` and the attribute `cf7_2_post_id`,
`
$args = array(
  'post_type'  => 'fault-post',
  'post_status'=> 'any',
  'author' => get_current_user_id()
);
$faults = get_posts($args);
foreach($faults as $post){
  $cf7_attr = ' cf7_2_post_id="'.$post->ID.'"';
  //display your form, you might want to add some more html to structure to display them as tabs or something else.
  echo do_shortcode('[cf7-2-post key="user-fault" title="Faults" '.$cf7_attr.']');
}
wp_reset_postdata();
//if you need to add an extra empty form, then ensure you pass the cf7_2_post_id attribute as -1
//$cf7_attr = ' cf7_2_post_id="-1"';
//echo do_shortcode('[cf7-2-post key="user-fault" title="Faults" '.$cf7_attr.']');
`
= I made a mistake in my form mapping, how do I correct it once it is created? =
as of v2.0.0 you can now quick-edit (inline edit) your form in the forms table listing and reset your form mapping to `draft` mode which will allow you to make changes.  Unless you have a fair understanding of WordPress posts and meta-fields structures and how these are saved in the database, I highly recommend that you delete any existing posts that may have been saved from form submissions that used the previous mappings.  Failing to do this without a proper understanding of the changes you are making to an existing mapping with previously saved post submissions could lead to difficult errors to debug and fix once you start creating post submissions that have a different mapping.  Consider yourself warned!

= I have enabled a save button on my form, but draft submissions are not being validated! =
This is the default functionality for saving draft submissions.  This is especially useful for avery large forms which users may take several visits to your site to complete.  Email notifications of draft submissions are also disabled.  If you wish to override this, you may do with the filters `cf7_2_post_draft_skips_validation` & `cf7_2_post_draft_skips_mail` examples of which are given in the documentation *Filters & Actions* below.

== Screenshots ==

1. You can map your form fields to post fields and meta-fields.  You can save the mapping as a draft.  You can also change the custom post attributes that will be used to create the post. The default ones are `public, show_ui, show_in_menu, can_export, has_archive, exclude_from_search`.  For more information, please consult the custom post [documentation](https://codex.wordpress.org/Function_Reference/register_post_type).
2. Once created, you have can only view the mapping.  All the fields are disabled to maintain post integrity. You can however add new meta-fields.  You will also see your new custom post in your dashboard menu is you have enabled post attributes `show_ui` & `show_in_menu`.
3. The CF7 table list shows an extra column with the status of the form mapping.
4. You can now map forms fields to custom taxonomies
5. You can edit your custom taxonomy nomenclature and slug, do this before mapping it.
6. If your form contains a file upload field, the featured-image option will appear on the mapping screen.  Select your file field to map the uploaded image to the post thumbnail.

== Changelog ==
= 2.0.0 =
* enabled UI for system posts mapping
* enabled reset mapping for created mappings
* introduced filters to skips mail & validation when saving draft forms
* added actions for plugin dev: cf7_2_post_form_posted
* added system post meta fields filter: cf7_2_post_skip_system_metakey
* added filter to display system post types: cf7_2_post_display_system_posts
= 1.5.0 =
* bug fix which prevented multiple taxonomies from being saved
* added autofill functionality on meta-field button creation.

= 1.4.0 =
* introduce cf7_2_post_id attribute in the cf7 shortcode to enable multiple forms in single page
= 1.3.2 =
* introduced extra filter for mapping taxonomies in system posts
* added filter 'cf7_2_post_map_extra_taxonomy' to add non-mapped taxonomy
* added filter 'cf7_2_post_pre_load-'{$post_type} to make use of post factory object

= 1.3.1 =
* small bug fix

= 1.3.0 =
* enable mapping to existing post types using hooks
* added filter 'cf7_2_post_form_values' to filter values loaded in form
* swapped jquery select2 for of chosen plugin
* added filter 'cf7_2_post_form_append_output' to allow custom scripts to be appended to forms
* added functionality to map taxonomies belonging to other existing posts
* introduced a save button in the cf7 elements to build draft submission forms
* fixed some minor bugs resulting from cf7 plugin update
* improved loading of mapped forms
* make use of 'do_shortcode_tag' filter introduced in WP4.7
* introduced a custom js event 'cf7Mapped' on the form to ensure custom scripts don't fire too early.

= 1.2.6 =
* bug fix which prevented files being uploaded properly

= 1.2.5 =
* bug fix which prevented files from being saved as custom meta fields in post

= 1.2.4 =
* added filter 'cf7_2_post_register_post_{post_type}' to allow tweaking of custom post registration

= 1.2.3 =
* changed hooking position of cf7 submission process to save forms to posts before mails are sent

= 1.2.2 =
* fixed a bug which prevented cf7 emails from being filled with field values

= 1.2.1 =
* small bug fix stopping cpt properties from being changed once created
* added filter

= 1.2.0 =

* ability to map custom taxonomies to fields
* new filter for the author field
* ability for logged in users to save a draft form and edit it later.
* fixed some bugs
* added some more hooks

= 1.1.0 =
* Auto deactivation of extension if CF7 plugin is deactivated

= 1.0 =
* Allows for mapping of any CF7 form to a custom post


== Filters & Actions ==
<div id="#documentation">
</div>
The following filters are provided in this plugin,

= `cf7_2_post_supports_{$post_type}` =

Set custom post type support attributes (see [documentation](https://codex.wordpress.org/Function_Reference/register_post_type#supports)),
`
add_filter('cf7_2_post_supports_quick-contact','set_supports');
function set_supports($default_supports){
  $default_supports[]='comments';
  return $default_supports;
}
`
= `cf7_2_post_capabilities_{$post_type}` =

Set [custom post capabilities](http://wordpress.stackexchange.com/questions/108338/capabilities-and-custom-post-types) for user access,
`
add_filter('cf7_2_post_capabilities_quick-contact','set_capabilities');
function set_capabilities($capabilities){
$capabilities = array(
    'edit_post' => 'edit_contact',
    'edit_posts' => 'edit_contacts',
    'edit_others_posts' => 'edit_others_contacts',
    'publish_posts' => 'publish_contacts',
    'read_post' => 'read_contacts',
    'read_private_posts' => 'read_private_contacts',
    'delete_post' => 'delete_contact'
);
  return $capabilities;
}
`
All capabilities must be set, else the plugin will default back to default `post` capabilities.  Also, make sure you assign each of these capabilities to the admin role (or other roles/users) else you won't be able to access your custom post.

= `cf7_2_post_form_mapped_to_{$post_type}` =

Action fired when a submitted form is saved to a new custom post, for example if your custom post type is `my-cpt`,

`
add_action('cf7_2_post_form_mapped_to_my-cpt','modify_form_posts',10,2);
function modify_form_posts($post_id, $cf7_form_data){
  //cf7_form_data is the submitted data from your form
  //post_id is the id of the post to which it has been saved.
  //... do something here
}
`
NOTE: all posts are saved in `draft` mode, so if you wanted this to be changed and published immediately, you could do it with the above example.

= `cf7_2_post_author_{$post_type}` =
Allows you to set a custom author ID for a new post based on the form being submitted.
`
add_filter('cf7_2_post_author_my-cpt','set_my_post_author',10,3);
function set_my_post_author($author_id, $cf7_form_id, $cf7_form_data){
  //$cf7_form_data is the submitted data from your form
  //$cf7_form_id is the id of the form being saved to a custom post my-cpt.
  //... do something here and set a new author ID
  return $author_id;
}
`
This filter expects the author ID to be returned.

= 'cf7_2_post_filter_taxonomy_registration-{$taxonomy_slug}' =
This filter allows you to customise [taxonomies arguments](https://codex.wordpress.org/Function_Reference/register_taxonomy#Arguments) before they are registered.
`
add_filter('cf7_2_post_filter_taxonomy_registration-my_categories','modify_my_categories');
function modify_my_categories($taxonomy_arg){
  //$taxonomy_arg is an array containing arguments used to register the custom taxonomy
  //modify the values in the array and pass it back
  //for example, by default all taxonomies are registered as hierarchical, use this filter to change this.
  $taxonomy_arg['hierarchical'] = false;
  return $taxonomy_arg;
}
`
It is possible to pass optional arguments for Metabox callback functions, taxonomy count update, and the taxonomy capabilities.  See the WordPress [register_taxonomy](https://codex.wordpress.org/Function_Reference/register_taxonomy) documentation for more information.

`
add_filter('cf7_2_post_filter_taxonomy_registration-my_categories','modify_my_categories');
function modify_my_categories($taxonomy_arg){
  $args = array(
          'meta_box_cb' => 'my_custom_taxonomy_metabox',
          'update_count_callback' => 'my_taxonomy_selected',
          'capabilities' => array(
                              'manage_terms' => 'manage_categories'
                              'edit_terms' => 'manage_categories'
                              'delete_terms' => 'manage_categories'
                              'assign_terms' => 'edit_posts'
                            )
        );
  return args;
}
`

= 'cf7_2_post_filter_cf7_field_value' =

This filter allows you to pre-fill form fields with custom values for **new submissions**.
`
add_filter('cf7_2_post_filter_cf7_field_value','modify_my_field',10,3);
function modify_my_field($value, $cf7_post_id, $field){
  //assuming you have defined a text field called city-location for cf7 form ID=20
  if(20 == $cf7_post_id && 'city-location' == $field){
    $value = 'London';
  }
  return $value;
}
`
= 'cf7_2_post_filter_cf7_taxonomy_terms' =

This filter allows you to pre-fill/select taxonomy terms fields for new submissions.
`
add_filter('cf7_2_post_filter_cf7_taxonomy_terms','modify_my_terms',10,3);
function modify_my_terms($terms_id, $cf7_post_id, $field){
  //assuming you have defined a checkbox field called city-locations for cf7 form ID=20
  if(20 == $cf7_post_id && 'city-locations' == $field){
    $term = get_term_by('name','London','location_categories');
    $terms_id = array();
    $terms_id[] = $term->term_id;
  }
  return $terms_id;
}
`
The filter expects an array of terms id.

= 'cf7_2_post_filter_taxonomy_query' =

This filter allows you to modify the taxonomy terms query arguments for a form's dropdown/checkbox/radio list.

`
add_filter('cf7_2_post_filter_taxonomy_query','custom_dropdown_order',10,3);
function custom_dropdown_order($args, $cf7_post_id, $taxonomy){
  if(20 == $cf7_post_id && 'location_categories' == $taxonomy){
    //modify the order in which the terms are listed,
    $args['order_by'] = 'count';
  }
  return $args;
}
`
This function changes the list order, putting the most commonly used terms at the top of the list.
For more information on taxonomy query arguments, please refer to the [WP codex documentation](https://developer.wordpress.org/reference/functions/get_terms/#parameters).

= 'cf7_2_post_filter_cf7_taxonomy_select2' =

This filter expects a boolean, by default it is `true` and enables [jquery select2 plugin](https://select2.github.io/) on select dropdown fields.
To disable it, do the following

`
add_filter('cf7_2_post_filter_cf7_taxonomy_select2','disable_select2_plugin',10,3);
function disable_select2_plugin($enable, $cf7_post_id, $form_field){
  if(20 == $cf7_post_id && 'your-option' == $form_field){
    //we assume here that cf7 form 20 has a dropdown field called 'your-option' which was mapped to a taxonomy
    $enable=false;
  }
  //you could just return false if you want to disable for all dropdown
  return $enable;
}
`
= 'cf7_2_post_filter_cf7_delay_select2_launch' =

This allows you manually launch the select2 jquery dropdonw fields.  This is required if you need to customise the select dropdown on windows load event with your own jquery scripts before the select2 transformation is applied.  Please read the FAQ on custom scripts to make sure you trigger your script after the form is mapped.
`
add_filter( 'cf7_2_post_filter_cf7_delay_select2_launch', '__return_true');`

= 'cf7_2_post_filter_cf7_taxonomy_select_optgroup' =

This filter expects a boolean, by default it is `false` and disables [`optgroup`](http://www.w3schools.com/tags/tag_optgroup.asp) on select dropdown options.
To enable grouped options for hierarchical taxonomy top level term, you can use this filter.  Note however, that child term options will be grouped by their top-level parent only as nested `optgroup` are not allowed. Furthermore the parent term will not be selectable. Therefore this option only makes sense if you have a hierarchical taxonomy with only single level child terms which can be selected.  To enable grouped options,

`
add_filter('cf7_2_post_filter_cf7_taxonomy_select_optgroup','enable_grouped_options',10,4);
function enable_grouped_options($enable, $cf7_post_id, $form_field, $parent_term){
  if(20 == $cf7_post_id && 'your-option' == $form_field){
    //we assume here that cf7 form 20 has a dropdown field called 'your-option' which was mapped to a hierarchical taxonomy
    //you can even filter it based on the parent term, so as to group some and not others.
    //the attribute $parent_term is a WP_Term object
    switch($parent_term->name){
      case 'Others':
        $enable=false;
        break;
      default:
        $enable=true;
        break;
    }
  }
  return $enable;
}
`

= `cf7_2_post_filter_user_draft_form_query` =
This filter is useful to change the behaviour in which previously submitted values can be edited by a user.  By default the plugin loads forms values that have been saved using the 'save' button.  However, you can modify this by changing the default post query such as the example below,
`
add_filter('cf7_2_post_filter_user_draft_form_query','load_published_submissions',10,2);
function load_published_submissions($query_args, $post_type){
  if('submitted-reports' == post_type){
    //we assume a cf7 form allowing users to submit online reports has been mapped to a post_type submitted-reports'
    if(is_user_logged_in()){
      $user = wp_get_current_user();
      //load this user's previously submitted values
      $query_args = array(
      	'posts_per_page'   => 1,
      	'post_type'        => post_type,
      	'author'	   => $user->ID,
      	'post_status'      => 'published'
      );
    }
  }
  return $query_args;
}
`

= `cf7_2_post_form_append_output` =

this filter is fired when the cf7 shortcode output is printed, it allows you to add a custom script at the end of your form should you need it,
`
add_filter('cf7_2_post_form_append_output', 'append_my_script', 10, 3);
function append_my_script($output, $attr, $nonce){
  if(!isset($attr['id'])){
    return $output;
  }
  $cf7_id = $attr['id'];
  if(19 == $cf7_id){ //check this is your form
    $output .= '<script type="text/javascript">';
    $output .= '(function( $ ) {';
    $output .= '  //fire your script once the form nonce event is triggered';
    $output .= '  $(document).on("'.$nonce.'", $("div#'.$nonce.' form.wpcf7-form"), function() {';
    $output .= '  var cf7Form = $("div#'.$nonce.' form.wpcf7-form");';
    $output .= '  ... //your custom scripting';
    $output .= '});';
    $output .= '})( jQuery );';
    $output .= '</script>';
  }
  return $output;
}
`

= `cf7_2_post_form_values` =
This filter allows you to load default values into your mapped forms. If the current user has a saved form, this filter will override any values you set.

`
add_filter('cf7_2_post_form_values', 'set_default_location', 10, 3);
function set_default_location($values, $$cf7_id, $mapped_post_type){
  if('travel_post' != mapped_post_type){
    return values;
  }
  if(19 == $cf7_id){ //check this is your form
    $field_name = 'location-rental';
    $values[$field_name] .= 'Paris';
  }
  return $values;
}
`
= 'cf7_2_post_register_post_{post_type}' =

this filter allows you to tweak the arguments used to register the custom_post type, for example, if you want to modify the [rewrite front-end slug](https://codex.wordpress.org/Function_Reference/register_post_type#rewrite) for the post type,

`add_filter('cf7_2_post_register_post_my-custom-post', 'set_rewrite_slug');
function set_rewrite_slug($args){
  $args['rewrite'] = array(
    'slug' => 'posted-replies',
    'with_front' => true
  );
  return $args;
}
`
= `cf7_2_post_map_extra_taxonomy` =

this filter allows you to add extra taxonomy to the list of mapped taxonomies.  This is useful when you are mapping your form to an existing post_type. Currently this is only possible using the hooks as the UI implementation will be done later on.  So in order to pre-load your form with taxonomy terms for a dropdown/check/radio field, you need to first register the taxonomy slug with the plugin,

`
//assume you have a form to post to your blog (post_type=post)
add_filter('cf7_2_post_map_extra_taxonomy', 'register_category',10,2);
function register_category( $taxonomies, $cf7_key){
  if($cf7_key != 'my-posted-form'){
    return $taxonomies;
  }
  //assume you have a field called your-category,
  //so users select a term from the category taxonomy
  $taxonomies['your-category'] = 'category';
  return $taxonomies;
}
`
= `cf7_2_post_pre_load-{$post_type}` =

using the above example, we now want to pre-load our form with the existing terms in the category taxonomy,
`
add_filter('cf7_2_post_pre_load-post', 'pre_load_taxonomy', 10,6);
function pre_load_taxonomy($post_values, $cf7_key, $cf7_2_post_factory){
  if($cf7_key != 'my-posted-form'){
    return $post_values;
  }
  //$cf7_2_post_factory is the internal factory object used to handle the mapping
  //the method, get_taxonomy_mapping($taxonomy_slug, $parent, $term_ids, $form_field)
  // is used to pre_load values in your field, and if you supply an array of term_ids, these will be pre-selected too.
  $post_values['your-category'] = $cf7_2_post_factory->get_taxonomy_mapping('category', 0, array(), 'your-category');

  return $post_values;
}
`
= `cf7_2_post_draft_skips_validation` =
For forms which have a save button, the validation of draft forms are skipped by default. This filter allows you to force validation of draft forms.

`add_fitler('cf7_2_post_draft_skips_validation', 'force_validation');
function force_validation($skip_validation, $cf7_key){
  if('my-form' == $cf7_key){
    skip_validation = false;
  }
  return skip_validation;
}
`
= `cf7_2_post_draft_skips_mail` =
For forms which have a save button, the mail sending of draft forms is skipped by default. This filter allows you to force mail notification of draft forms.

`add_fitler('cf7_2_post_draft_skips_mail', 'force_notification');
function force_notification($skip_mail, $cf7_key){
  if('my-form' == $cf7_key){
    skip_mail = false;
  }
  return skip_mail;
}
`
= `cf7_2_post_display_system_posts` =
In v2.0 the plugin allows users to map their forms to existing system posts.  By default, only system posts which are visible in the dashboard are listed.  This list can be modified by this filter,

`add_filter('cf7_2_post_display_system_posts', 'filter_posts', 10, 2);
function filter_posts($displayed_posts, $form_id){
  // the form_id is the post id of the current cf7 form being mapped
  //displayed_posts is an array of $post_type => $post_label key value pairs
  return displayed_posts;
}`

= `cf7_2_post_skip_system_metakey` =
In v2.0 the plugin allows users to map their forms to existing system posts through a UI interface.  The form fields can be mapped to the post fields, as well as existing post meta-fields, in addition to being able to add new ones too.  The list of existing meta-fields available is built by ignoring meta-fields with names starting with the '_' character which by convention is used to denote an internal meta-field.  This filter permits to include these meta-fields on a field by field mode,
`add_filter('cf7_2_post_skip_system_metakey', 'filter_post_metas', 10, 3);
function filter_post_metas($skip, $post_type, $meta_field_name){
  // boolean $skip flag is set to true by default
  //the $post_type of the post to which the form is being mapped to
  //$meta_field_name is the name of the field which is being skipped.
  return $skip;
}`


= `cf7_2_post_form_posted` =

action introduced for plugin developers specifically.  Fired at the end of the submission mapping process, once a new post has been created for a new submission.  The current mapping of the form fields is exposed, along with the data values submitted in the form and the files uploaded.  For developers interested in using this hook, please lookup in the inline documentation in the code itself.  The action is located in the includes/class-cf7-2-post-factory.php file.

* added system post meta fields filter:
* added filter to display system post types:
== Upgrade Notice ==
As of now there is no special upgrade notes, simply  follow the normal plugin update process.
