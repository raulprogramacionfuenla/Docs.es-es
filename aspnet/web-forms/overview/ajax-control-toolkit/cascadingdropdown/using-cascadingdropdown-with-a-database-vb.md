---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-vb
title: Usar CascadingDropDown con una base de datos (VB) | Documentos de Microsoft
author: wenz
description: El control CascadingDropDown en el Kit de herramientas de Control de AJAX extiende un control DropDownList para que los cambios en una carga de DropDownList asociados valores de anoth...
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 97a3d33c-c856-43f3-8acb-f1ccbc48221a
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-vb
msc.type: authoredcontent
ms.openlocfilehash: 65b9a499dd9b500338ccdb90e56b742ff50a1024
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/10/2017
---
<a name="using-cascadingdropdown-with-a-database-vb"></a><span data-ttu-id="6b057-103">Usar CascadingDropDown con una base de datos (VB)</span><span class="sxs-lookup"><span data-stu-id="6b057-103">Using CascadingDropDown with a Database (VB)</span></span>
====================
<span data-ttu-id="6b057-104">por [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="6b057-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="6b057-105">[Descargar código](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.vb.zip) o [descarga de PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="6b057-105">[Download Code](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.vb.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1VB.pdf)</span></span>

> <span data-ttu-id="6b057-106">El control CascadingDropDown en el Kit de herramientas de Control de AJAX extiende un control DropDownList para que los cambios en una carga de DropDownList asociados valores en otra DropDownList.</span><span class="sxs-lookup"><span data-stu-id="6b057-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="6b057-107">En orden para que funcione, debe crearse un servicio web especial.</span><span class="sxs-lookup"><span data-stu-id="6b057-107">In order for this to work, a special web service must be created.</span></span>


## <a name="overview"></a><span data-ttu-id="6b057-108">Información general</span><span class="sxs-lookup"><span data-stu-id="6b057-108">Overview</span></span>

<span data-ttu-id="6b057-109">El control CascadingDropDown en el Kit de herramientas de Control de AJAX extiende un control DropDownList para que los cambios en una carga de DropDownList asociados valores en otra DropDownList.</span><span class="sxs-lookup"><span data-stu-id="6b057-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="6b057-110">(Por ejemplo, una lista proporciona una lista de US Estados y la lista siguiente, a continuación, se rellena con ciudades importantes en ese estado.) En orden para que funcione, debe crearse un servicio web especial.</span><span class="sxs-lookup"><span data-stu-id="6b057-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) In order for this to work, a special web service must be created.</span></span>

## <a name="steps"></a><span data-ttu-id="6b057-111">Pasos</span><span class="sxs-lookup"><span data-stu-id="6b057-111">Steps</span></span>

<span data-ttu-id="6b057-112">En primer lugar, es necesario un origen de datos.</span><span class="sxs-lookup"><span data-stu-id="6b057-112">First of all, a data source is required.</span></span> <span data-ttu-id="6b057-113">Este ejemplo utiliza la base de datos de AdventureWorks y Microsoft SQL Server 2005 Express Edition.</span><span class="sxs-lookup"><span data-stu-id="6b057-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="6b057-114">La base de datos es una parte opcional de una instalación de Visual Studio (incluida la edición express) y también está disponible como una descarga independiente en [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span><span class="sxs-lookup"><span data-stu-id="6b057-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="6b057-115">La base de datos de AdventureWorks es parte de los ejemplos de SQL Server 2005 y bases de datos de ejemplo (descargue en [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang = es](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="6b057-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="6b057-116">La manera más fácil de configurar la base de datos es usar Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx? FamilyID = c243a5ae 4bd1 4e3d 94b8 5a0f62bf7796&amp;DisplayLang = es](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) y adjuntar la `AdventureWorks.mdf` archivo de base de datos.</span><span class="sxs-lookup"><span data-stu-id="6b057-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="6b057-117">En este ejemplo, se supone que se llama a la instancia de SQL Server 2005 Express Edition `SQLEXPRESS` y reside en el mismo equipo que el servidor web; también es la configuración predeterminada.</span><span class="sxs-lookup"><span data-stu-id="6b057-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="6b057-118">Si el programa de instalación diferente, tendrá que adaptar la información de conexión para la base de datos.</span><span class="sxs-lookup"><span data-stu-id="6b057-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="6b057-119">Para activar la funcionalidad de AJAX de ASP.NET y el Kit de herramientas de Control, el `ScriptManager` control se debe colocar en cualquier sitio en la página (pero en el &lt; `form` &gt; elemento):</span><span class="sxs-lookup"><span data-stu-id="6b057-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the &lt;`form`&gt; element):</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample1.aspx)]

<span data-ttu-id="6b057-120">En el paso siguiente, se necesitan dos controles de DropDownList.</span><span class="sxs-lookup"><span data-stu-id="6b057-120">In the next step, two DropDownList controls are required.</span></span> <span data-ttu-id="6b057-121">En este ejemplo, usamos la información de contacto y proveedor de AdventureWorks, por lo tanto, creamos una lista para los proveedores disponibles y otra para los contactos disponibles:</span><span class="sxs-lookup"><span data-stu-id="6b057-121">In this sample, we use the vendor and contact information from AdventureWorks, thus we create one list for the available vendors and one for the available contacts:</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample2.aspx)]

<span data-ttu-id="6b057-122">A continuación, dos extensores CascadingDropDown deben agregarse a la página.</span><span class="sxs-lookup"><span data-stu-id="6b057-122">Then, two CascadingDropDown extenders must be added to the page.</span></span> <span data-ttu-id="6b057-123">Uno rellena la primera lista (proveedores) y el otro llena la segunda lista (contactos).</span><span class="sxs-lookup"><span data-stu-id="6b057-123">One fills the first (vendors) list, and the other one fills the second (contacts) list.</span></span> <span data-ttu-id="6b057-124">Se deben establecer los siguientes atributos:</span><span class="sxs-lookup"><span data-stu-id="6b057-124">The following attributes must be set:</span></span>

- <span data-ttu-id="6b057-125">`ServicePath`: Dirección URL de un servicio web entrega las entradas de lista</span><span class="sxs-lookup"><span data-stu-id="6b057-125">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="6b057-126">`ServiceMethod`: Método web entrega de las entradas de lista</span><span class="sxs-lookup"><span data-stu-id="6b057-126">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="6b057-127">`TargetControlID`: Id. de la lista desplegable</span><span class="sxs-lookup"><span data-stu-id="6b057-127">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="6b057-128">`Category`: Información de categoría que se envía al método web cuando se llama</span><span class="sxs-lookup"><span data-stu-id="6b057-128">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="6b057-129">`PromptText`: Texto que aparece cuando asincrónicamente Cargando datos de la lista desde el servidor</span><span class="sxs-lookup"><span data-stu-id="6b057-129">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>
- <span data-ttu-id="6b057-130">`ParentControlID`: (opcional) que la carga de los desencadenadores de la lista actual de lista desplegable elemento primario</span><span class="sxs-lookup"><span data-stu-id="6b057-130">`ParentControlID`: (optional) parent dropdown list that triggers loading of the current list</span></span>

<span data-ttu-id="6b057-131">Según el lenguaje de programación utilizado, cambiará el nombre del servicio web en cuestión, pero todos los demás valores de atributo son los mismos.</span><span class="sxs-lookup"><span data-stu-id="6b057-131">Depending on the programming language used, the name of the web service in question changes, but all other attribute values are the same.</span></span> <span data-ttu-id="6b057-132">Este es el elemento CascadingDropDown para la primera lista desplegable:</span><span class="sxs-lookup"><span data-stu-id="6b057-132">Here is the CascadingDropDown element for the first dropdown list:</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample3.aspx)]

<span data-ttu-id="6b057-133">Los extensores de control para la segunda lista necesitan establecer el `ParentControlID` atributo para que al seleccionar una entrada en los desencadenadores de la lista de proveedores de carga asociadas a elementos de la lista de contactos.</span><span class="sxs-lookup"><span data-stu-id="6b057-133">The control extenders for the second list need to set the `ParentControlID` attribute so that selecting an entry in the vendors list triggers loading associated elements in the contacts list.</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample4.aspx)]

<span data-ttu-id="6b057-134">A continuación, se realiza el trabajo real en el servicio web, que se configura como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="6b057-134">The actual work is then done in the web service, which is set up as follows.</span></span> <span data-ttu-id="6b057-135">Tenga en cuenta que el `[ScriptService]` se usa el atributo, en caso contrario, AJAX de ASP.NET no se puede crear el proxy de JavaScript para tener acceso a los métodos web desde el código de script del lado cliente.</span><span class="sxs-lookup"><span data-stu-id="6b057-135">Note that the `[ScriptService]` attribute is used, otherwise ASP.NET AJAX cannot create the JavaScript proxy to access the web methods from client-side script code.</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-vb/samples/sample5.aspx)]

<span data-ttu-id="6b057-136">La firma de los métodos web llamado a CascadingDropDown es como sigue:</span><span class="sxs-lookup"><span data-stu-id="6b057-136">The signature of the web methods called by CascadingDropDown is as follows:</span></span>

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample6.vb)]

<span data-ttu-id="6b057-137">Por lo que el valor devuelto debe ser una matriz de tipo `CascadingDropDownNameValue` que se define mediante el Kit de herramientas de Control.</span><span class="sxs-lookup"><span data-stu-id="6b057-137">So the return value must be an array of type `CascadingDropDownNameValue` which is defined by the Control Toolkit.</span></span> <span data-ttu-id="6b057-138">El `GetVendors()` método es bastante fácil de implementar: el código se conecta a la base de datos de AdventureWorks y consulta los primeros 25 proveedores.</span><span class="sxs-lookup"><span data-stu-id="6b057-138">The `GetVendors()` method is quite easy to implement: The code connects to the AdventureWorks database and queries the first 25 vendors.</span></span> <span data-ttu-id="6b057-139">El primer parámetro de la `CascadingDropDownNameValue` constructor es el título de la entrada de la lista, la segunda se su valor (atributo value del HTML &lt; `option` &gt; elemento).</span><span class="sxs-lookup"><span data-stu-id="6b057-139">The first parameter in the `CascadingDropDownNameValue` constructor is the caption of the list entry, the second one its value (value attribute in HTML's &lt;`option`&gt; element).</span></span> <span data-ttu-id="6b057-140">Este es el código:</span><span class="sxs-lookup"><span data-stu-id="6b057-140">Here is the code:</span></span>

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample7.vb)]

<span data-ttu-id="6b057-141">Obtener los contactos asociados para un proveedor (nombre del método: `GetContactsForVendor()`) es un poco más complicado.</span><span class="sxs-lookup"><span data-stu-id="6b057-141">Getting the associated contacts for a vendor (method name: `GetContactsForVendor()`) is a bit trickier.</span></span> <span data-ttu-id="6b057-142">En primer lugar, debe determinarse el proveedor que se ha seleccionado en la primera lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="6b057-142">First of all, the vendor which has been selected in the first dropdown list must be determined.</span></span> <span data-ttu-id="6b057-143">El Kit de herramientas de Control define un método auxiliar para dicha tarea: el `ParseKnownCategoryValuesString()` método devuelve un `StringDictionary` elemento con los datos de la lista desplegable:</span><span class="sxs-lookup"><span data-stu-id="6b057-143">The Control Toolkit defines a helper method for that task: The `ParseKnownCategoryValuesString()` method returns a `StringDictionary` element with the dropdown data:</span></span>

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample8.vb)]

<span data-ttu-id="6b057-144">Por motivos de seguridad, estos datos deben validarse en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="6b057-144">For security reasons, this data must be validated first.</span></span> <span data-ttu-id="6b057-145">Por tanto, si hay una entrada de proveedor (dado que la `Category` propiedad del primer elemento CascadingDropDown está establecida en `"Vendor"`), se puede recuperar el Id. del proveedor seleccionado:</span><span class="sxs-lookup"><span data-stu-id="6b057-145">So if there is a Vendor entry (because the `Category` property of the first CascadingDropDown element is set to `"Vendor"`), the ID of the selected vendor may be retrieved:</span></span>

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample9.vb)]

<span data-ttu-id="6b057-146">El resto del método es bastante sencilla, a continuación.</span><span class="sxs-lookup"><span data-stu-id="6b057-146">The rest of the method is fairly straight-forward, then.</span></span> <span data-ttu-id="6b057-147">Id. del proveedor se utiliza como un parámetro para una consulta SQL que recupera todos los contactos asociados para ese proveedor.</span><span class="sxs-lookup"><span data-stu-id="6b057-147">The vendor's ID is used as a parameter for an SQL query that retrieves all associated contacts for that vendor.</span></span> <span data-ttu-id="6b057-148">Una vez más, el método devuelve una matriz de tipo `CascadingDropDownNameValue`.</span><span class="sxs-lookup"><span data-stu-id="6b057-148">Once again, the method returns an array of type `CascadingDropDownNameValue`.</span></span>

[!code-vb[Main](using-cascadingdropdown-with-a-database-vb/samples/sample10.vb)]

<span data-ttu-id="6b057-149">Cargar la página ASP.NET y, después de un breve período de tiempo se rellena la lista de proveedores con 25 entradas.</span><span class="sxs-lookup"><span data-stu-id="6b057-149">Load the ASP.NET page, and after a short while the vendor list is filled with 25 entries.</span></span> <span data-ttu-id="6b057-150">Seleccione una entrada y observe cómo la segunda lista desplegable se rellena con datos.</span><span class="sxs-lookup"><span data-stu-id="6b057-150">Pick one entry and notice how the second dropdown list is filled with data.</span></span>


<span data-ttu-id="6b057-151">[![La primera lista se rellena automáticamente](using-cascadingdropdown-with-a-database-vb/_static/image2.png)](using-cascadingdropdown-with-a-database-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6b057-151">[![The first list is filled automatically](using-cascadingdropdown-with-a-database-vb/_static/image2.png)](using-cascadingdropdown-with-a-database-vb/_static/image1.png)</span></span>

<span data-ttu-id="6b057-152">La primera lista se rellena automáticamente ([haga clic aquí para ver la imagen a tamaño completo](using-cascadingdropdown-with-a-database-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="6b057-152">The first list is filled automatically ([Click to view full-size image](using-cascadingdropdown-with-a-database-vb/_static/image3.png))</span></span>


<span data-ttu-id="6b057-153">[![La segunda lista se rellena según la selección en la primera lista](using-cascadingdropdown-with-a-database-vb/_static/image5.png)](using-cascadingdropdown-with-a-database-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="6b057-153">[![The second list is filled according to the selection in the first list](using-cascadingdropdown-with-a-database-vb/_static/image5.png)](using-cascadingdropdown-with-a-database-vb/_static/image4.png)</span></span>

<span data-ttu-id="6b057-154">La segunda lista se rellena según la selección en la primera lista ([haga clic aquí para ver la imagen a tamaño completo](using-cascadingdropdown-with-a-database-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="6b057-154">The second list is filled according to the selection in the first list ([Click to view full-size image](using-cascadingdropdown-with-a-database-vb/_static/image6.png))</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="6b057-155">[Anterior](filling-a-list-using-cascadingdropdown-vb.md)
[Siguiente](presetting-list-entries-with-cascadingdropdown-vb.md)</span><span class="sxs-lookup"><span data-stu-id="6b057-155">[Previous](filling-a-list-using-cascadingdropdown-vb.md)
[Next](presetting-list-entries-with-cascadingdropdown-vb.md)</span></span>