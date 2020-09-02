# Rails application development usefull tricks

Generate a rails secret key:
```
bundle exec rake secret
```

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
u1.save(validate: false)
```

Execute SQL query using ActiveRecord:
```
# Need to verify
results = ActiveRecord::Base.connection.execute("SELECT * FROM users") 
```

Check list of model classes:
```
ActiveRecord::Base.connection.tables.map do |model|
  model.capitalize.singularize.camelize
end
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

Active record query to fetch data using only matching with date from datetime filed:
```
scope :day, -> (start_date) {where("DATE(start_date) = ?", start_date)}
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

Cancan ability user can be able to update their own password only:
```
can [:change_password, :update_password], User, user_id: user.id  
```

Sum of array of objects attribute values:
```
class Product

  def initialize(id, name, price)
    @id = id
    @name = name
    @price = price
  end
end

products = []
p1 = Product.new(1, 'Shirt',20)
p2 =Product.new(2, 'T-Shirt', 30)
products << p1
products << p2
total = products.sum(&:price)
p total
```

Filter with ajax based from submission:
Form:
```
= form_for(:user, url: users_path, method: :get, html: { id: 'user-form', class: '', remote: true }) do |f|
  .col-md-2.form-group
    = f.label 'From Date'
    = f.text_field :from_date, class: 'form-control', placeholder: 'YYYY-MM-DD', value: from_date
  .col-md-2.form-group
    = f.label 'To Date'
    = f.text_field :to_date, class: 'form-control', placeholder: 'YYYY-MM-DD', value: to_date
  .col-md-2.form-group
    = blank_space
    = f.submit 'Search', id: 'search-button', class: 'btn btn-info btn-block'
```

Jquery:
```
$(document).ready(function() {
  var load_data = function(form_data={}) {
    $.ajax({
      url: '/users/search',
      type: 'GET',
      data: form_data,
      beforeSend: function() {},
      success: function(response) {
        console.log(response);
      },
      error: function(xhr) {
        console.log('Failed!');
      }
    });
  };

  // Filter by form submit
  $("#user-form").submit(function(e) {
    e.preventDefault();

    var form = $(this);
    var url = form.attr('action');
    load_data(form.serialize());
  });

});
```

Usefull directory format to follow:
- Use YYYYMMDD format for naming a directory to keep the versioning of static data files. 
- In this format directories will be automatically sorted as ascending order of number.
- Example- 20200601, 20200602, 20200603, 20200604, 20200605, 20200606 etc.
- Ruby script: ```Time.now.strftime('%Y%m%d')```

Unique elements based on a attribute value from array of objects:
```
```

Downlaod as CSV file:
"Model class method
"Model instance method by default


TODO: Data importing form files XLS, XLSX or CSV using ```roo``` gem:
- File read from datewise folder:


TODO: Graph plot using chartJS:


Unzip a zipped file:
```
source_path = Rails.root.join('data', 'blogs.zip').to_s
destination_path = Rails.root.join('data', 'blog')


Zip::File.open(source_path) do |zip_file|
  zip_file.each do |file|
    puts file.name
    f_path = File.join(destination_path, file.name)
    zip_file.extract(file, f_path) unless File.exist? (f_path)
  end
end
```

Benchmarking of a code block execution time:
```
require 'benchmark'

def get_files
  time = Benchmark.measure do
    pdf_files = PdfParser.pdf_files()
  end
  puts time.real
end
```

### Gemfile environment group:
If you don't need some gems in your locally then make it a group gems explicitely by environment like below
```
group :production, :staging do
  gem install dbi
  gem install ruby-oci8
end
```

In my case i was not able to install ruby-oci8 gem due to the oracle instant client istallation error LD_LIBRARY_PATH not set error locall that's why i was not able to run the app and deploy anything on prod/staging env. my solution was to ignore instalation of ruby-oci8 gem locally as i was able to install this gem in my prod environment.

After that have to make sure you run bundle install command without production and staging block:
```
$ bundle install --without production staging
```

### Make Empty a file using ruby

```
File.open('/tmp/file.txt', 'w') {|file| file.truncate(0) }
```
or
```
file = File.open(file_path, 'w')
file.truncate(0)
file.close()
```

To truncate a file:
```
File.truncate('/path/to/file', 0)
```
To truncate list of files:
```
[file1, file2, file3].each { |file| File.truncate(file, 0) }
```

### Export or write files as CSV in a particular rails app directory:
```
users = User.all
attributes = %w{ id first_name last_name user_name email address mobile created_at updated_at }
export_path = Rails.root.join('data', 'users.csv')
# Clear or empty if there is an existing file
File.open(export_path, 'wb') { |file| file.truncate(0) }

CSV.open(export_path, 'wb') do |csv|
  csv << attributes.map(&:upcase)

  users.each do |user|
    csv << attributes.map { |attr| user.send(attr) }
  end
end
```

