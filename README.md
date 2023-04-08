## Node Academy

Forked from [abhinavs' moonwalk theme](https://github.com/abhinavs/moonwalk)

## Quick Installation
1. [Fork this repository](https://github.com/VancouverBitdevs/nodeacademy/fork).
2. `cd nodeacademy`
3. `bin/bootstrap`

If you are installing this repository on Windows, please note that you might have to use Ruby 3.0.x instead of Ruby 3.1.x - you can see Windows specific installation instructions [here](https://github.com/abhinavs/moonwalk/blob/master/moonwalk_on_windows.md)

## Starting Server
`bin/start` - development server will start at http://127.0.0.1:4000

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/abhinavs/moonwalk.

## Development

To set up your environment to develop this theme, run `bundle install`.

Your theme is setup just like a normal Jekyll site! To test your theme, run `bundle exec jekyll serve` and open your browser at `http://localhost:4000`. This starts a Jekyll server using your theme. Add pages, documents, data, etc. like normal to test your theme's contents. As you make modifications to your theme and to your content, your site will regenerate and you should see the changes in the browser after a refresh, just like normal.

When your theme is released, only the files in `_layouts`, `_includes`, `_sass` and `assets` tracked with Git will be bundled.
To add a custom directory to your theme-gem, please edit the regexp in `moonwalk.gemspec` accordingly.

## Acknowledgement
This theme's original base is [no style please!](https://github.com/riggraz/no-style-please) theme created by  [Riccardo Graziosi](https://riggraz.dev/) - many thanks to him for creating a wonderful theme with nearly no css. 

## License

The theme is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).
