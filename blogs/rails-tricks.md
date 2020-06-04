# Rails application development usefull tricks

Connect database from rails console and execute sql queries:
```
$ bundle exec rails dbconsole
```

Truncate a db table data from rails console:
```
User.connection.truncate(User.table_name)
```

Create model(user seed) data without validation:
```
u1 = User.new(name: 'admin', email: "admin@example.com", mobile_number: '01912107357', password: 'Admin@123', password_confirmation: 'Admin@123', allowed_to_log_in: true)
u1.save(false)
```

Ruby/Rails class(model) private class method:
```

def self.parse_data_file
  []
end

private_class_method :parse_data_file
```

Range of dates:
```
(1.week.ago.to_date..Date.today.to_date).map{ |day| day.strftime('%Y-%m-%d') }
```

Active record query to fetch data using date time range(last 1 weeks data):
```
users = User.where(created_at: 1.week.ago..Date.today)
```

Search with multiple form fileds(attributes):
```
user = User
user = user.where(email: params[:email]) unless params[:email].blank?
user = user.where(first_name: params[:first_name]) unless params[:first_name].blank?
user = user.where(last_name: params[:last_name]) unless params[:last_name].blank?
user = user.where(mobile: params[:mobile]) unless params[:mobile].blank?

users = user.order('id DESC')
```

Multi-Select SQL generator:
```
def self.build_multi_select_sql(attr, str, seperator=',')
  arr = str.split(seperator)
  sql = ''

  arr.each_with_index do |e, i|
    sql = sql + "#{attr} = \'#{e.strip}\'"

    unless arr[i+1].nil?
      sql = sql + ' OR '
    end
  end

  return sql
end
```

Call and build query on top of above method:
```
users = User.where(self.build_multi_select_sql('thana', params[:thana], ',')) unless params[:thana].blank?
```

Search form:
```
- name = params[:commit] == 'Search' ? params[:user][:name] : ''
- division = params[:commit] == 'Search' ? params[:user][:division] : ''
- district = params[:commit] == 'Search' ? params[:user][:district] : ''
- thana = params[:commit] == 'Search' ? params[:user][:thana] : ''

.alert.alert-warning{role: 'alert'}
  Use comma(,) separated values for Name multiple select(Example - Masud, Rana, John)

.row
  = form_for(:user, url: search_users_path, method: :get, html: { class: '' }) do |f|
    .col-md-1.form-group
      = f.label 'Name'
      = f.text_field :name, class: 'form-control', value: name
    .col-md-1.form-group
      = f.label 'Division'
      = f.select(:division, options_for_select(User::DIVISIONS.collect {|n| [n, n]}, division), {:include_blank => 'Select'}, { :class => 'form-control' })
    .col-md-1.form-group
      = f.label 'District'
      = f.text_field :district, class: 'form-control', value: district
    .col-md-1.form-group
      = f.label 'Thana'
      = f.text_field :thana, class: 'form-control', value: thana
    .col-md-2.form-group
      = blank_space
      = f.submit 'Search', class: 'btn btn-info btn-block'
```

