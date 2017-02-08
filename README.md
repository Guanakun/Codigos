# Codigos

package escuelita_java;

import java.math.BigDecimal;
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.Iterator;
import java.util.List;

public class SuperMercado {

	List<Producto> productoList = new ArrayList<Producto>();

	public SuperMercado() {
		initProductList();
	}

	private void initProductList() {

		this.productoList.add(new Producto("Coca Cola Zero", new BigDecimal(20), "Litros 1.5"));
		this.productoList.add(new Producto("Coca Cola", new BigDecimal(18), "Litros: 1.5"));
		this.productoList.add(new Producto("Shampoo Sedal", new BigDecimal(30), "Contenido: 500mm"));
		this.productoList.add(new Producto("Frutillas", new BigDecimal(64), "Unidad de venta: kilo"));

	}

	/**
	 * @return the productList
	 */
	public List<Producto> getProductList() {
		return productoList;
	}

	/**
	 * @param productList
	 *            the productList to set
	 */
	public void setProductList(List<Producto> productList) {
		this.productoList = productList;
	}

	private Producto getCheapest() {

		Producto producto = Collections.min(productoList, Comparator.comparing(p -> p.getPrice()));

		return producto;
	}

	private Producto getMoreExpensive() {

		Producto producto = Collections.max(productoList, Comparator.comparing(p -> p.getPrice()));

		return producto;
	}

	public void printInfo() {
		productoList.forEach(producto -> System.out.println(
				"Nombre: " + producto.getName() + "///" + producto.getPrice() + "$///" + producto.getInfoArticulo()));
		System.out.println("===================================================================================");
		System.out.println("producto mas caro :" + this.getMoreExpensive().getName());
		System.out.println("producto mas barato :" + this.getCheapest().getName());

	}

}
