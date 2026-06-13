# Note:
I dropped the folder into the repository after completing it. But for some reason, GitHub can't read drag-and-dropped folders. So you'll have to go through the ZIP file.

# Project Title
Very Epic Gallery

# Description
This is an art gallery that mainly features all of the drawings made on quizzes. I hope you like this.

# Main Features
* Search and sorting. The sorting uses the .map method which is very helpful.
* Admin panel for admin users
* Being able to upload your own artwork. They don't have to be part of exhibitions, but each of them can also be added to multiple.
* Distinction between regular users and registered artists. Registered artists have an artist icon next to their profiles. You can hover over them to see the tooltip.
* You can comment and favorite specific pieces of art.
* You can upload your own profile photos, including GIF files which is funny.
* Users can delete their own artwork and comments
* Admin panel allows manual approval of artworks to specific exhibitions
* You can sign in/out.
* There is a custom Mp3 embed in the nav bar which I like. I like this music and I hope you like it too. However, I could not figure out how to make the music persist as you navigate between pages.

# Models and Associations

## User
- `has_many :sessions`
- `has_one :artist`
- `has_many :favorites`
- `has_many :favorite_artworks`, through: `:favorites`, source: `:artwork`
- `has_many :comments`
- `has_many :exhibition_artworks`, as `submitted_by` (`submitted_by_id`)
- `has_one_attached :avatar`

## Artist
- `belongs_to :user` (optional — an artist profile can exist without a linked account)
- `has_many :artworks`

## Artwork
- `belongs_to :artist`
- `has_many :favorites`
- `has_many :favorited_by`, through: `:favorites`, source: `:user`
- `has_many :comments`
- `has_many :exhibition_artworks`
- `has_many :exhibitions`, through: `:exhibition_artworks`
- `has_one_attached :image`

## Exhibition
- `has_many :exhibition_artworks`
- `has_many :artworks`, through: `:exhibition_artworks`

## ExhibitionArtwork (the join model)
- `belongs_to :exhibition`
- `belongs_to :artwork`
- `belongs_to :submitted_by`, class_name: `"User"`
- `status` enum: `pending`, `approved`, `rejected` (admin approval workflow)

## Comment
- `belongs_to :user`
- `belongs_to :artwork`

## Favorite
- `belongs_to :user`
- `belongs_to :artwork`

## Session
- `belongs_to :user`

# How to run this gallery web app
Do the following in your terminal
```bash
rails db:seed
rails s
```

# How to log in as user/admin
All of the passwords are "password"

| Role  | Email               
|-------|---------------------
| Admin | admin@example.com
| User  | yuan@example.com
| User  | bob@example.com
| User  | jemian@example.com
| User  | billfoot@example.com

## Main URLs

- `/` — artwork browse (aka the home page)
- `/exhibitions` — exhibitions
- `/account/profile/edit` — account settings, artist profile, and artworks
- `/admin` — admin dashboard

# Known limitations
* I mentioned earlier that the Mp3 in the nav bar doesn't persist across pages.
* For some reason CSS acts weird in Rails. I tried to make the nav bar sticky so it persists as the user scrolls down. But it does not work.
