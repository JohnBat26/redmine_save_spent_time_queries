= redmine_save_spent_time_queries



Compatible with Redmine 2.3.x



First we need modify /app/views/timelog/_date_range.html.erb to add "Save" button to Spent time form



```html


<div id="query_form_content" class="hide-when-print">
  <fieldset id="filters" class="collapsible <%= @query.new_record? ? "" : "collapsed" %>">
    <legend onclick="toggleFieldset(this);"><%= l(:label_filter_plural) %></legend>
    <div style="<%= @query.new_record? ? "" : "display: none;" %>">
      <%= render :partial => 'queries/filters', :locals => {:query => @query} %>
    </div>
  </fieldset>
  <fieldset class="collapsible collapsed">
    <legend onclick="toggleFieldset(this);"><%= l(:label_options) %></legend>
    <div style="display: none;">
      <table>
        <tr>
          <td><%= l(:field_column_names) %></td>
          <td><%= render_query_columns_selection(@query) %></td>
        </tr>
      </table>
    </div>
  </fieldset>
</div>

<p class="buttons hide-when-print">
  <%= link_to_function l(:button_apply), 'submit_query_form("query_form")', :class => 'icon icon-checked' %>
  <%= link_to l(:button_clear), {:project_id => @project, :issue_id => @issue}, :class => 'icon icon-reload'  %>
  <a class="icon icon-save" href="#" onclick="$('#query_form').attr('action', 'spent_time_query/new'); submit_query_form('query_form'); return false;">Save</a>
</p>

<div class="tabs">
<% query_params = params.slice(:f, :op, :v, :sort) %>
<ul>
    <li><%= link_to(l(:label_details), query_params.merge({:controller => 'timelog', :action => 'index', :project_id => @project, :issue_id => @issue }),
                                       :class => (action_name == 'index' ? 'selected' : nil)) %></li>
    <li><%= link_to(l(:label_report), query_params.merge({:controller => 'timelog', :action => 'report', :project_id => @project, :issue_id => @issue}),
                                       :class => (action_name == 'report' ? 'selected' : nil)) %></li>
</ul>
</div>


```



Copy source to /plugins/redmine_save_spent_time_queries


Run rake redmine:plugins:migrate


Restart Redmine
