# Activeadmin-and-Devise-setup
# paste this three gems

    gem "paperclip", "~> 6.0.0"
    gem 'activeadmin'
    gem 'devise'
    
#next lets bundle
    
    bundle
    
#install devise first

    rails g devise:install
    past the localhost:3000 into the development enviroment
    optional* generate devise views
    
#install active_admin

    rails g active_admin:install
    run rake db:migrate
    
#create a deafult user
        
    rails c
    AdminUser.create!(email:"admin@example.com",password:"password",password_confirmation:"password")
    
    
# call in models you made
for example... 

    rails g model customfields fields:string
    rake db:migrate
    rails g active_admin:resource customfield   (singular dont know why but if you use customfields and run migrate you will get errors)
    rake db:migrate
    rails s
    
#inside the admin section:
paste this and change the details 

    permit_params :title, :description
      form do |f|
        f.inputs do
          f.input :title , :label => "Field name"
          f.input :description, :label => "Upload an image"
        end
        f.actions
      end
     end
     
#if you installed paperclip into your model here a checklist

    rails g paperclip customfields image
    rake db:migrate
    
paste this into customfields model file
    
    validates :fields, presence: true
    
    has_attached_file :image, styles: { medium: "300x300>", thumb: "100x100>" }
    validates_attachment_content_type :image, content_type: /\Aimage\/.*\z/
    
 #inside your forms
    
     f.input :image, :label => "Upload an image"

#editor for active admin

     gem 'active_admin_editor'
     //= require active_admin/editor/wysiwyg
     $ rails g active_admin:editor
     
     ActiveAdmin.register Page do
  form do |f|
    f.inputs do
      f.input :title
      f.input :content, as: :html_editor
    end

    f.buttons
  end
end
    
