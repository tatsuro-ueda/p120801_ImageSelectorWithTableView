The purpose of this sample project is to select image by table view.

This is selection table view.

![selection](http://farm8.staticflickr.com/7121/7691053062_4d28e97275_o.png)

And this is detail view.

![detail](http://farm9.staticflickr.com/8288/7691053254_14ab538469_o.png)

At first, I made property `arrayImg`.

    - (id)initWithCoder:(NSCoder *)aDecoder
    {
        self = [super initWithCoder:aDecoder];
        if (self) {
            self.arrayImg = [NSArray arrayWithObjects:
                             [UIImage imageNamed:@"image0.jpg"],
                             [UIImage imageNamed:@"image1.jpg"],
                             [UIImage imageNamed:@"image2.jpg"], nil];
        }
        return self;
    }

Then, I wrote the cell selection code.

    - (void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath
    {
        NSString *s = [NSString stringWithFormat:@"image%d.jpg", indexPath.row];
        [self performSegueWithIdentifier:@"showImage" sender:s];
    }

At last, I made `prepareForSegue` method.

    - (void)prepareForSegue:(UIStoryboardSegue *)segue sender:(id)sender
    {
        DetailViewController *d = segue.destinationViewController;
        d.strImgName = sender;
    }

In the detail view, I just wrote below:

    - (void)viewWillAppear:(BOOL)animated
    {
        self.imageView.image = [UIImage imageNamed:strImgName];
    }