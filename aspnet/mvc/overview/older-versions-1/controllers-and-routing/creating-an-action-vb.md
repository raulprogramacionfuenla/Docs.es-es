---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
title: Creación de una acción (VB) | Microsoft Docs
author: microsoft
description: Obtenga información sobre cómo agregar una nueva acción a un controlador ASP.NET MVC. Obtenga información sobre los requisitos para un método que se trata de una acción.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: c8d93e11-ef78-4a30-afbc-f30419000a60
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
msc.type: authoredcontent
ms.openlocfilehash: 070dd4c9d68327eec52fe385000b9ca3907eaa9f
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "41824061"
---
<a name="creating-an-action-vb"></a>Creación de una acción (VB)
====================
por [Microsoft](https://github.com/microsoft)

> Obtenga información sobre cómo agregar una nueva acción a un controlador ASP.NET MVC. Obtenga información sobre los requisitos para un método que se trata de una acción.


El objetivo de este tutorial es explicar cómo puede crear una nueva acción de controlador. Conozca los requisitos de un método de acción. También aprenderá cómo impedir que un método que se expone como una acción.

## <a name="adding-an-action-to-a-controller"></a>Agregar una acción a un controlador

Agregar una nueva acción a un controlador mediante la adición de un nuevo método al controlador. Por ejemplo, el controlador en el listado 1 contiene una acción denominada Index() y una acción denominada SayHello(). Ambos métodos se exponen como acciones.

**Listado 1 - Controllers\HomeController.vb**

[!code-vb[Main](creating-an-action-vb/samples/sample1.vb)]

Con el fin de exponerse al universo como una acción, un método debe cumplir ciertos requisitos:

- El método debe ser público.
- El método no puede ser un método estático.
- El método no puede ser un método de extensión.
- El método no puede ser un constructor de captador o establecedor.
- El método no puede tener tipos genéricos abiertos.
- El método no es un método de la clase base del controlador.
- El método no puede contener **ref** o **out** parámetros.

Tenga en cuenta que no hay ninguna restricción en el tipo de valor devuelto de una acción del controlador. Una acción de controlador puede devolver una cadena, un valor DateTime, una instancia de la clase Random, o void. El marco ASP.NET MVC convertirá cualquier tipo de valor devuelto no es un resultado de acción en una cadena y procesar la cadena en el explorador.

Cuando se agrega a cualquier método que no infrinja estos requisitos a un controlador, el método se expone como una acción de controlador. Tenga cuidado aquí. Cualquier persona conectada a Internet puede invocar una acción de controlador. No, por ejemplo, cree una acción de controlador DeleteMyWebsite().

## <a name="preventing-a-public-method-from-being-invoked"></a>Impide que se invoca un método público

Si necesita crear un método público en una clase de controlador y no desea exponer el método como una acción de controlador, a continuación, puede impedir que el método que se invoca mediante el uso de la &lt;NonAction&gt; atributo. Por ejemplo, el controlador en el listado 2 contiene un método público denominado CompanySecrets() decorada con el &lt;NonAction&gt; atributo.

**Listado 2 - Controllers\WorkController.vb**

[!code-vb[Main](creating-an-action-vb/samples/sample2.vb)]

Si se intenta invocar la acción del controlador CompanySecrets() escribiendo /Work/CompanySecrets en la barra de direcciones del explorador, a continuación, obtendrá el mensaje de error en la figura 1.


[![Invocar un método NonAction](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)

**Figura 01**: invocar un método NonAction ([haga clic aquí para ver imagen en tamaño completo](creating-an-action-vb/_static/image2.png))

> [!div class="step-by-step"]
> [Anterior](creating-a-controller-vb.md)
> [Siguiente](aspnet-mvc-controllers-overview-cs.md)
