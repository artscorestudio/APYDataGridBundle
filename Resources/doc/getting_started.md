Getting Started With APYDataGridBundle
======================================

## Choose your source of data

You can choose between an [Entity (ORM)][1], a [Document (ODM)][2] or a [Vector (Array)][3] source.

### Entity (ORM)

```php
<?php
// AppBundle\DefaultController.php
namespace AppBundle\Controller;

use APY\DataGridBundle\Grid\Source\Entity;

class DefaultController extends Controller
{
    public function myGridAction()
    {
        // Creates simple grid based on your entity (ORM)
        $source = new Entity('AppBundle:MyEntity');
        ...
    }
}
```
[Learn more about Entity (ORM)][1].

### Document (ODM)

```php
<?php
// AppBundle\DefaultController.php
namespace AppBundle\Controller;

use APY\DataGridBundle\Grid\Source\Document;

class DefaultController extends Controller
{
    public function myGridAction()
    {
        // Creates simple grid based on your document (ODM)
        $source = new Document('AppBundle:MyDocument');
        ...
    }
}
```
[Learn more about Document (ODM)][2].

### Vector (Array)

```php
<?php
// AppBundle\DefaultController.php
namespace AppBundle\Controller;

use APY\DataGridBundle\Grid\Source\Vector;

class DefaultController extends Controller
{
    public function myGridAction()
    {
        $data = array(
            array(
                'id' => 1,
                'title' => 'book1',
                'publication' => '2012-04-06'
            ),
            array(
                'id' => 2,
                'title' => 'book2',
                'publication' => 'Apr. 6, 2012'
            ),
        );

        // Creates simple grid based on your data
        $source = new Vector($data);
        ...
    }
}
```

[Learn more about Vector (Array)][3].

## Get a grid instance

```php
<?php
public function myGridAction()
{
    ...
    $grid = $this->get('grid');
    ...
}
```

## Attach the source to the grid

```php
<?php
public function myGridAction()
{
    ...
    $grid = $this->get('grid');

    $grid->setSource($source);
    ...
}
```

## Configuration of the grid

```php
<?php
public function myGridAction()
{
    ...
    $grid->setSource($source);

    // Set the identifier of the grid
    // Add a column
    // Show/Hide columns
    // Set default filters
    // Set the default order
    // Set the default page
    // Set max results
    // Set prefix titles
    // Add mass actions
    // Add row actions
    // Manipulate the query builder
    // Manipulate rows data
    // Manipulate columns
    // Manipulate column render cell
    // Set items per page selector
    // Set the data for Entity and Document sources
    // Exports
    ...
}
```

## Return the grid to the template

```php
<?php
public function myGridAction()
{
    ...
    $grid->setSource($source);

    // Prepare data and the grid

    $grid->isReadyForRedirect();

    // Configuration of the grid

    return $this->render('AppBundle::grid.html.twig', array('grid' => $grid));
    ...
}
```

## Manage the grid redirection, exports and the response of the controller

```php
<?php
public function myGridAction()
{
    ...
    $grid->setSource($source);

    // Configuration of the grid

    return $grid->getGridResponse('AppBundle::grid.html.twig');
    ...
}
```

See [grid response][4] for more informations.

## Complete example with an entity source

```php
<?php
// AppBundle\DefaultController.php
namespace AppBundle\Controller;

use APY\DataGridBundle\Grid\Source\Entity;

class DefaultController extends Controller
{
    public function myGridAction()
    {
        // Creates simple grid based on your entity (ORM)
        $source = new Entity('AppBundle:MyEntity');

        // Get a grid instance
        $grid = $this->get('grid');

        // Attach the source to the grid
        $grid->setSource($source);

        // Configuration of the grid

        // Manage the grid redirection, exports and the response of the controller
        return $grid->getGridResponse('AppBundle::grid.html.twig');
    }
}
```

[1]: source/entity_source.md
[2]: source/document_source.md
[3]: source/vector_source.md
[4]: grid_configuration/grid_response.md